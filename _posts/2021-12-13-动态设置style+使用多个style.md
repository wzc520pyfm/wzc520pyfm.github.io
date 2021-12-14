---
layout: post
title: '动态设置style+使用多个style'
subtitle: 'vue中动态设置style以及使用多个style'
date: 2021-12-13
categories: 技术
author: lalala
cover: ''
tags: 前端
---

### 使用多个style

```html
<div :style="[AStyle, BStyle]">
```

这在封装组件时很有用, 当你希望通过父组件传来style对象, 进而改变组件内的style时, 就会用到.

### 动态设置style

```html
<!-- vue中动态设置style -->
<div :style="{ fontSize: postFontSize + 'em', color: 'red' }">
```

