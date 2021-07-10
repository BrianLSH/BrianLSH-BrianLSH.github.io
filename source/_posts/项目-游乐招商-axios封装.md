---
title: 楼市早讯
tags: Vue 项目 后台管理
toc: true
date: 2020-04-20
categories:
- [Vue, 项目, 游乐招商]
---

### 楼市早讯登录功能总结
 
#### axios 封装 
```css
可以挂载到原型对象上组建中通过this访问
此项目我们把每一个请求都封装成一个一个的独立功能函数，
在需要的时候加载调用即可
```
#### 登录功能

```js
/**
 * 用户相关的请求模块
 */
import request from "@/utils/request";

/**
 * 用户登录
 */
export const login = data => {
  return request({
    method: 'POST',
    url: '/app/v1_0/authorizations',
    data
  })
}


/*
然后在登录页面中加载调用用户登录
 */

import { login } from "@/api/user";

async onLogin () {
  // const loginToast = this.$toast.loading({
  this.$toast.loading({
    duration: 0, // 持续时间，0表示持续展示不停止
    forbidClick: true, // 是否禁止背景点击
    message: '登录中...' // 提示消息
  })

  try {
+    const res = await login(this.user)
    console.log('登录成功', res)
    // 提示 success 或者 fail 的时候，会先把其它的 toast 先清除
    this.$toast.success('登录成功')
  } catch (err) {
    console.log('登录失败', err)
    this.$toast.fail('登录失败，手机号或验证码错误')
  }
}
```


#### token处理 存储在VueX

```js
1、在 `src/store/index.js` 中

import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    // 登录用户，一个对象，包含 token 信息
+    user: null
  },
  mutations: {
+    setUser (state, data) {
+      state.user = data
+    }
  },
  actions: {
  },
  modules: {
  }
})

2、登录成功以后将后端返回的 token 相关数据存储到容器中

async onLogin () {
  // const loginToast = this.$toast.loading({
  this.$toast.loading({
    duration: 0, // 持续时间，0表示持续展示不停止
    forbidClick: true, // 是否禁止背景点击
    message: '登录中...' // 提示消息
  })

  try {
    const res = await login(this.user)

    // res.data.data => { token: 'xxx', refresh_token: 'xxx' }
+    this.$store.commit('setUser', res.data.data)

    // 提示 success 或者 fail 的时候，会先把其它的 toast 先清除
    this.$toast.success('登录成功')
  } catch (err) {
    console.log('登录失败', err)
    this.$toast.fail('登录失败，手机号或验证码错误')
  }

  // 停止 loading，它会把当前页面中所有的 toast 都给清除
  // loginToast.clear()
}

```
#### 持久化 token 存储

```js
Vuex 容器中的数据只是为了方便在其他任何地方能获取登录状态数据，
但是页面刷新还是会丢失数据状态，所以我们还要把数据进行持久化中
以防止页面刷新丢失状态的问题。
前端持久化常见的方式就是：

- 本地存储
- Cookie

这里我们以使用本地存储持久化用户状态为例。

为了方便，这里先封装一个用于操作本地存储的工具模块。

1、创建 src/utils/storage.js

export const getItem = name => {
  return JSON.parse(window.localStorage.getItem(name));
};

export const setItem = (name, value) => {
  return window.localStorage.setItem(name, JSON.stringify(value));
};

export const removeItem = name => {
  window.localStorage.removeItem(name);
};

2、然后在容器中使用使用本地存储持久化 token 数据

import Vue from 'vue'
import Vuex from 'vuex'
+ import { setItem, getItem } from '@/utils/storage'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    // 登录用户，一个对象，包含 token 信息
+    user: getItem('user')
    // user: null
  },
  mutations: {
    setUser (state, data) {
      state.user = data

      // 为了防止刷新丢失 state 中的 user 状态，我们把它放到本地存储
+      setItem('user', state.user)
    }
  },
  actions: {
  },
  modules: {
  }
})

```

#### 使用请求拦截器统一添加 token

```js
...
// 在非组件模块中访问容器，直接 import 加载即可
import store from '@/store'

// 请求拦截器
request.interceptors.request.use(
  function (config) {
    const user = store.state.user
    if (user) {
      // 注意：后端要求 Bearer 后面有个空格，多了少了都不行
      // Authorization 也是后端要求的名字，不能乱写
      config.headers.Authorization = `Bearer ${user.token}`
    }
    // Do something before request is sent
    return config
  },
  function (error) {
    // Do something with request error
    return Promise.reject(error)
  }
)
```


#### 处理 token 过期 实现无缝刷新

```js
参考
https://emacle.github.io/posts/vue-token-guo-qi-wu-feng-shua-xin/
https://blog.csdn.net/djzhao627/article/details/101193213
在响应中需要进行Token的校验，失效后进行Token的刷新并重发请求
请求重发的注意点是，使用响应里的config作为参数进行重发

在请求的响应拦截器中统一处理 token 过期

/**
 * 封装 axios 请求模块
 */
import axios from "axios";
import jsonBig from "json-bigint";
import store from "@/store";
import router from "@/router";

// axios.create 方法：复制一个 axios
const request = axios.create({
  baseURL: "http://ttapi.research.itcast.cn/" // 基础路径
});

/**
 * 配置处理后端返回数据中超出 js 安全整数范围问题
 */
request.defaults.transformResponse = [
  function(data) {
    try {
      return jsonBig.parse(data);
    } catch (err) {
      return {};
    }
  }
];

// 请求拦截器
request.interceptors.request.use(
  function(config) {
    const user = store.state.user;
    if (user) {
      config.headers.Authorization = `Bearer ${user.token}`;
    }
    // Do something before request is sent
    return config;
  },
  function(error) {
    // Do something with request error
    return Promise.reject(error);
  }
);

// 响应拦截器
request.interceptors.response.use(
  // 响应成功进入第1个函数
  // 该函数的参数是响应对象
  function(response) {
    // Any status code that lie within the range of 2xx cause this function to trigger
    // Do something with response data
    return response;
  },
  // 响应失败进入第2个函数，该函数的参数是错误对象
  async function(error) {
    // Any status codes that falls outside the range of 2xx cause this function to trigger
    // Do something with response error
    // 如果响应码是 401 ，则请求获取新的 token

    // 响应拦截器中的 error 就是那个响应的错误对象
    console.dir(error);
    if (error.response && error.response.status === 401) {
      // 校验是否有 refresh_token
      const user = store.state.user;

      if (!user || !user.refresh_token) {
        router.push("/login");

        // 代码不要往后执行了
        return;
      }

      // 如果有refresh_token，则请求获取新的 token
      try {
        const res = await axios({
          method: "PUT",
          url: "http://ttapi.research.itcast.cn/app/v1_0/authorizations",
          headers: {
            Authorization: `Bearer ${user.refresh_token}`
          }
        });

        // 如果获取成功，则把新的 token 更新到容器中
        console.log("刷新 token  成功", res);
        store.commit("setUser", {
          token: res.data.data.token, // 最新获取的可用 token
          refresh_token: user.refresh_token // 还是原来的 refresh_token
        });

        // 把之前失败的用户请求继续发出去
        // config 是一个对象，其中包含本次失败请求相关的那些配置信息，例如 url、method 都有
        // return 把 request 的请求结果继续返回给发请求的具体位置
        return request(error.config);
      } catch (err) {
        // 如果获取失败，直接跳转 登录页
        console.log("请求刷线 token 失败", err);
        router.push("/login");
      }
    }

    return Promise.reject(error);
  }
);

export default request;
```

#### 登录成功跳转回原来页面

```js
在响应中需要进行Token的校验，失效后进行Token的刷新并重发请求
请求重发的注意点是，使用响应里的config作为参数进行重发
```
#### 头像更新--eventBus

```js

// 公共实例
import Vue from 'vue'
export default new Vue() // 公共实例 => 实例化了一个Vue


  // 认为保存成功 => 通知header组件 更新信息
    eventBus.$emit('updateUserInfo')

   eventBus.$on('updateUserInfo', () => {
        // 认为别人更新了数据 自己也应该更新
        this.getUserInfo()
      })
```
#### 素材轮播展示--carousel

```css
carsouel 是懒加载的  第一次没有弹出之前  是没有组件元素的
即使拿到index 也没法用，因为不知道什么时间加载完，什么时间要用

dialog 的open 方法， 不能用，不知道什么时间渲染完成，所以用opened

轮播逻辑
dialog 渲染 list 里面的数据
点击时转存索引  通过opened事件 用 ref调用文档中的api setActiveItem（索引实现跳转）
```
#### 

```js
```
#### 

```js
```
#### 

```js
```