---
title: CSS案例
toc: true
tags: CSS基础 CSS案例 伪类
date: 2015-05-11
categories:
  - [CSS, 案例]
---

### 导航条中间加 '|'
```css
<style>
          * {
                margin: 0px;
                list-style: none;
             }
             
        .nav {
            width: 100%;
            overflow: hidden;
       padding-top: 20px;
            /* 水平垂直居中 */
             /* position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%,-50%);  */
        }
        ul {
            padding-left: 180px;
        }
      
        ul li {
            float: left;
        }

        li+li::before {
           margin: 0px 10px;
           content: '|';
       }
    </style>
       
 <div class="nav">
        <ul>
            <li>小米商城</li>
            <li>华为商城</li>
            <li>锤子</li>
            <li>vivo</li>
            <li>oppo</li>
        </ul>
    </div>
```