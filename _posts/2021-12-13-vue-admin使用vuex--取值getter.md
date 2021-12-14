---
layout: post
title: 'vue-admin使用vuex--取值getter'
subtitle: 'vue-element-admin封装了很好的vuex取值方法,getter'
date: 2021-12-13
categories: 技术
author: lalala
cover: ''
tags: 前端
---



### vue-admin使用vuex--取值getter

* store/modules/app.js(已省略无关代码)

  ```js
  const state = {
    sidebar: {
      opened: true
    }
  }
  export default {
    namespaced: true,
    state
  }
  ```

* store/getters.js(已省略无关代码)

  ```js
  const getters = {
    sidebar: state => state.app.sidebar
  }
  export default getters
  ```

* store.index.js(已省略无关代码)

  ```js
  import Vue from 'vue'
  import Vuex from 'vuex'
  import getters from './getters'
  import app from './modules/app'
  Vue.use(Vuex)
  const store = new Vuex.Store({
    modules: {
      app
    },
    getters,
  })
  export default store
  ```

* 在经过封装后, 我们就可以通过getters来获取app里state的值, 像下面这样:

  ```js
  console.log(this.$store.getters.sidebar.opened)
  ```

  

