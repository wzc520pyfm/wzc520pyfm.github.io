---
layout: post
title: '覆盖ElementUI的样式'
subtitle: 'ElementUI的默认样式无法满足需求怎么办?'
date: 2021-12-13
categories: 技术
author: lalala
cover: ''
tags: 前端
---

### 覆盖ElementUI的样式

由于 element-ui 的样式我们是在全局引入的，所以你想在某个页面里面覆盖它的样式就不能加 scoped，但你又想只覆盖这个页面的 element 样式，你就可在它的父级加一个 class，用命名空间来解决问题。

```scss
.article-page {
  /* 你的命名空间 */
  .el-tag {
    /* element-ui 元素*/
    margin-right: 0px;
  }
}
```

**注意, 不能再使用scoped了, 另写一个style标签, 因为使用的css类名是编译后的css类名**



### 或者直接从浏览器查看要修改部分的class名, 直接对其进行修改, 当然了,这样你可能会看到一些长相奇怪的class名

```css
<style lang="scss">
// fix css style bug in open el-dialog
.el-popup-parent--hidden {
  .fixed-header {
    padding-right: 15px;
  }
}
</style>
```

