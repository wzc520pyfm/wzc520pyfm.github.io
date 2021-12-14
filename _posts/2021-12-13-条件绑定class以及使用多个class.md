---
layout: post
title: '条件绑定class以及使用多个class'
subtitle: 'vue中根据条件展示不同的样式,这时就需要使用条件绑定class'
date: 2021-12-13
categories: 技术
author: lalala
cover: ''
tags: 前端
---

### 条件绑定class以及使用多个class

```vue
<template>
<!--当isUseA为true时,AClass才会生效,否则只生效BClass-->
  <div :class="[{AClass,isUseA}, BClass]"></div>
<!--除了上面的对象写法外,也支持三目写法-->
   <div :class="[isUserA ? AClass : BClass]">
</template>
<script>
export default {
  data() {
    return {
      isUseA: true,
      AClass: 'AClass'
      BClass: 'BClass'
    }
  },
</script>
<style lang="scss">
    .AClass {
        
    }
    .BClass {
        
    }
</style>
```

