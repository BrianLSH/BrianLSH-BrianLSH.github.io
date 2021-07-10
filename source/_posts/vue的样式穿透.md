---
title: vue的样式穿透
toc: true
tags: Vue 样式穿透 深度作用域 
date: 2019-08-31
categories:
- [Vue, 基础]
---
### vue深度作用域
#### vue有 在有作用域样式的组建中，默认只能对作用域组件的根节点进行生效
```js
<根组件>
    <子组件>
        <子子组件>
        
        </子子组件 class="a">
    </子组件>
</根组件>

此时 样式a只能作用在根节点组件,要想作用在子组件可用以下解决办法。


1.脱离作用域，去掉scoped 但是容易和其他组件样式冲突
2. /deep/` 或者 `::v-deep`  >>>
详细见文档----> loader --->作用域样式 深度作用域
```

```css
/deep/ .abc {
   position: fixed;
     margin：10px;
     padding: 20px;
}

```
