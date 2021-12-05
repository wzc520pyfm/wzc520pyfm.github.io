### 使用vue-cli3.x的UI可视化界面创建项目

1. vue ui

   <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211010153348385.png" alt="image-20211010153348385" style="zoom: 67%;" />

2. 点击创建项目后:  ( 如果你选yarn 卡住创建不了项目的话还是乖乖用npm吧 )

   <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211010153615280.png" alt="image-20211010153615280" style="zoom: 67%;" />

3. 进行配置

   <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211010153806012.png" alt="image-20211010153806012" style="zoom:67%;" />

4. 选择配置: ( 练习项目, 仅选择下列几项即可, ESLint css预处理  TypeScript都是未来需要了解的 )

   * <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211010154051573.png" alt="image-20211010154051573" style="zoom:67%;" />

   * <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211010154113170.png" alt="image-20211010154113170" style="zoom:67%;" />

   * <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211010154133170.png" alt="image-20211010154133170" style="zoom:67%;" />

   * <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211010154151774.png" alt="image-20211010154151774" style="zoom:67%;" />

   * <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211010154212842.png" alt="image-20211010154212842" style="zoom:67%;" />

5. 是否使用history

   <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211010154446711.png" alt="image-20211010154446711" style="zoom:67%;" />

6. 进行创建( UI界面看不到创建进度, 需要到vscode终端下看 )

   这时可以将配置保存, 也可不保存

   <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211010154537385.png" alt="image-20211010154537385" style="zoom:67%;" />

7. vue-cli3.x的架构在 '仿京东实战' 中已介绍过, 需要补充的是vue.config.js中的配置: 

   ```js
   // 常用配置
   module.exports = {
       //基本路径, vue-cli3.3以前请使用baseUrl
       publicPath: '/',
       //输出文件目录
       outputDir: 'dist',
       //用于嵌套生成的静态资产(js,css,img,fonts)的目录
       assetsDir: '',
       //todo 生成环境sourceMap--生成map文件,用于定位css或js哪里出错了,生成环境中一般不需要(改为false可显著减小打包体积)
       productionSourceMap: true,
       //webpack配置
       configureWebpack: () => {},
       chainWebpack: () => {},
       //css相关配置
       css: {
           //启用 CSS modules
           modules: false,
           //是否使用css分离插件
           extract: true,
           //开启 CSS source map? --用于定位错误,选为false可减小打包体积
           sourceMap: false,
           //css预设器(预处理器)配置项
           loaderOptions: {},
       },
       //webpack-dev-server 相关配置
       devServer: {
           //host: '0.0.0.0',//将服务启动在 0.0.0.0 的ip下
           port: 9528, //服务启动所在的端口
           open: true, //启动项目后自动打开浏览器
           proxy: {},//设置代理--产生跨域问题就可以在这里配置代理,这时webpack-dev-server就会在本地启动一个服务器来转发请求以解决跨域问题(服务器与服务器之间通信是没有跨域的,只有客户端和服务器间才会产生跨域)
       },
       //第三方插件配置
       pluginOptions: {
   
       }
   }
   ```

   

### vue组件间传值

* 父子组件传值----3种方法

  * props / $emit

    * 父传子:  props

    ```vue
    //父组件中
            <!--//* 传值--传的是 msg  加上 : 表示的是绑定了一个变量(会将""中的内容认为是一个变量), 如果不写则默认是字符串 -->
            <!--//todo 也就是说, 如果绑定的值是一个字符串的时候就不需要写 :  -->
            <m-child v-bind:msg=" 'from Parent msg' "></m-child>
            <m-child str="from Parent str"></m-child>
    ```

    ```vue
    //子组件中
    	<h5>{{msg}}</h5>
    	<h5>{{str}}</h5>
    <script>
    export default {
    	props: {
            msg: {
                type: String,
                default: ''
            },
            str: {
                type: String,
                default: ''
            }
        },
    }
    </script>
    ```
    * 子传父 :  $emit

    ```vue
    //子组件中
    <button @click="passMsg">走你!</button>
    <script>
    export default {
    	methods: {
            passMsg() {
                // 向父组件传值--第一个参数是事件名,第二个参数就是要传过去的参数
                this.$emit('showMsg', 'i am from Child');
            }
        },
    }
    </script>
    ```

    ```vue
    //父组件中
    		<m-child @showMsg="myShowMsg"></m-child>
            <!--//todo @不仅仅可以监听点击事件clcik, 还可以监听自定义的事件,比如showMsg,到监听到的时候执行myShowMsg -->
            <h3>{{msg}}</h3>
    <script>
    export default {
    	data() {
            return { msg: ''};
        },
    	methods: {
            //todo 你仅需要在template中写@showMsg="myShowMsg"即可,无需写明参数, vue会自动获得传来的参数
            myShowMsg(val) {
                this.msg = val
            }
        },
    }
    </script>
    ```

  * $parent / children

    ```js
    //获取子组件中的childMsg变量--方法一:通过$children(子组件获取父组件是$parent)
            console.log(this.$children[0].childMsg)
    ```

  * $ref

    ```vue
    <m-child ref="child"></m-child>
    <script>
        ...
        //获取子组件中的childMsg变量--方法二:本质同方法一, 为子组件指定了一个ref变量(类似id),通过$refs
            console.log('ref',this.$refs.child.childMsg)
    </script>
    ```

* 非父子组件传值

  * 事件总线   --其原理就是建立一个公共js文件, 专门用来传递消息

    1. 在src下新建utils文件夹, 在utils下新建bus.js

       ```js
       import Vue from 'vue'
       export default new Vue
       ```

    2. 在需要传递消息的地方引入bus.js

       ```js
       //one.vue中
       import bus from '../utils/bus'
       //two.vue中
       import bus from '../utils/bus'
       ```

    3. 传递消息

       ```vue
       //one.vue中
       <button @click="passMsg">传你</button>
       <script>
           methods: {
           passMsg() {
             bus.$emit('msg','i an from app')
           },
         },
       </script>
       ```

    4. 接收消息

       ```vue
       //two.vue中
       <h6>{{childMsg}}</h6>
       <script>
           data() {
               return { childMsg: 'child_msg' };
           },
           mounted() {
               bus.$on('msg', (val) => {
                   this.childMsg = val
               })
           },
       </script>
       ```

  * $attrs / $listeners

    **可以解决多级组件间传值的问题**

    **$attrs将父组件中不包含props的属性传入子组件, 通常配合interitAttrs选项一起使用**

    **$listeners监听子组件中数据变化, 传递给父组件**

    ==示例结构:  在App在中使用了Parent组件,在Parent组件中使用了Child组件==

    ***现在准备利用$attrs从App中传值到Child***

    1. 在App.vue中: 

       ```vue
       <m-parent :msga="a" :msgb="b" :msgc="c"></m-parent>
       <script>
           data(){
           return {
             a: 'msga',
             b: 'msgb',
             c: 'msgc'
           }
         },
       </script>
       ```

    2. 在Parent.vue中

       ```vue
       <m-child v-bind="$attrs"></m-child>
       <!-- 这里的v-bind不能用简写 -->
       ```

    3. 在Child.vue中

       ```js
       console.log(this.$attrs)
       //浏览器输出:
       //msga: "msga"
       //msgb: "msgb"
       //msgc: "msgc"
       //! 这里注意: 如果在Child中有一个名为msga的计算属性, 那么vue会过滤掉传来的msga, 浏览器只输出msgb和msgc
       ```

    ***现在准备利用$listeners获取子组件传来的值***

    1. 在Child.vue中

       ```js
       mounted() {
            this.$emit("childInfo","这是Child发送的信息")
       },
       ```

    2. 在Parent.vue中

       ```vue
       <m-child v-on="$listeners"></m-child>
       ```

    3. 在App.vue中

       ```vue
       <m-parent @childInfo="getInfo"></m-parent>
       <script>
         methods: {
           getInfo(data) {
             console.log(data)
               //浏览器输出:  这是Child发送的信息
           }
         },
       </script>
       ```

* vuex



### 单页面应用控制中心vue-router

* 路由的基本配置

  * router/index.js

    ```js
    const routes = [
      {
        path: '/home',
        component: () => import('../views/Home.vue')
      }
    ]
    ```

  * App.vue中

    ```vue
    <routerview></routerview>
    ```

    **要在App.vue中加上router-view才能显示路由**

* 路由的跳转

  * router-link

    ```vue
    //在App.vue中加:
    <router-link to="/home">go home</router-link>
    ```

  * 编程式导航

    ```vue
    <button @click="toHome">go Home</button>
    
    //跳转Home页
    toHome() {
        this.$router.push({path: '/home'})
    }
    ```

* 动态路由

  ```js
  //配置: 
  const routes = [
    {
      path: '/home/:id',
      name: 'home',
      component: () => import('../views/Home.vue')
    }
  ]
  ```

  ```vue
  //在Home.vue中获取参数
  <h1>{{$route.params.id}}</h1>
  ```

  ```
  浏览器输入: http://localhost:9528/#/home/2
  
  //使用代码传参跳转:(有以下两种写法, path与query一起用, name与params一起用)
  // this.$router.push({path: '/home', query: {name: 'Jack'} })
     this.$router.push({name: 'home', params: {id: 3} })
  ```

* 嵌套路由

  ```js
  //配置: 
  const routes = [
    {
      path: '/home/:id',
      component: () => import('../views/Home.vue'),
      children: [{
        path: '/child',
        component: () => import('../views/Child.vue')
      }]
    }
  ]
  ```

  ```
  //浏览器输入:
  http://localhost:9528/#/home/child
  ```

* 导航守卫

  ```js
  //在main.js中
  router.beforeEach((to, from, next) => {
    console.log(to.path)
    next()
  })
  ```

* 路由懒加载



### 状态管理中心--vuex的基础用法(官方文档是标准)

* State
  * 数据

* Mutations
  * 数据怎么改变

* Actions
  * 异步改变

![image-20211011100716691](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211011100716691.png)

* 使用示例: 

  * 在store/index.js中

    ```js
    import Vue from 'vue'
    import Vuex from 'vuex'
    
    Vue.use(Vuex)
    
    export default new Vuex.Store({
      state: {
        count: 0,
      },
      mutations: {  //通过commit来操作里面的方法
        add(state) {
          state.count ++
        },
        decrease(state) {
          state.count --
        }
      },
      actions: {  //通过dispatch来操作里面的方法
        delayAdd(context) {
          setTimeout(() => {
            context.commit('add')
          }, 1000);
        }
      },
      modules: {
      }
    })
    ```

  * 在组件中: 

    ```vue
    <h5>vuex:{{count}}</h5>
    <script>
    //? vuex中的数据都是通过计算属性获得的
        computed: {
            count() {
                return this.$store.state.count
            }
        },
    </script>
    ```

  * 如果有多个vuex中数据需要使用呢? 当然有简便的方法: 

    ```js
    //利用辅助函数实现, vuex中所有的辅助函数都以map开头
    import { mapState } from 'vuex'
    // computed: 
        //     mapSate({
        //  写法一       // count: state => state.count,
        //  写法二       count: 'count'
        //     }),
    	//  写法三
        computed:{
            ...mapState({
                count:'count'
            })
        },
    ```

  * 改变vuex中数据

    ```vue
    <h5>vuex:{{count}}</h5>
    <button @click="add">增加</button>
    <script>
    add() {
        this.$store.commit('add') //调用vuex中同步方法
        this.$store.dispatch('delayAdd')  //调用vuex中异步方法
    }
    </script>
    ```

  * ***(额外) 更好的写法***

    ```js
    mutations: {
    	increment (state, payload) {
            state.count += payload.amount
        }
    }
    ```

    ```js
    store.commit('increment', {
        amount: 10
    })
    //或者
    store.commit({
        type: 'increment',
        amount: 10
    })
    ```

    

### 状态管理中心vuex的高级用法

* getters

  ```js
  //store/index.js中
  getters: {
      //里面的每个方法都接收一个参数 state 来获取公告库中的数据
      doubleCount(state) {
        return state.count * 2;
      },
    },
  ```

  ```vue
  <h5>getters:<span>{{doubleCount}}</span></h5>
  <script>
  computed:{
          ...mapState({
              count:'count'
          }),
          doubleCount() {
              return this.$store.getters.doubleCount
          }
      },
  </script>        
  ```

  getters也可以通过辅助函数的方式使用:

  ```js
  import { mapState, mapGetters } from 'vuex'
  computed:{
          ...mapState({
              count:'count'
          }),
          //数组的形式的话, 属性名必须与store中保持一致
          ...mapGetters([
              'doubleCount'
          ])
          //如果你想为它另取一个名字的话, 需要传对象
          // ...mapGetters({
          //     newName: 'doubleCount'
          // })
      },
  ```

* ***模块化概念***

  1. 

  <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211011111522646.png" alt="image-20211011111522646" style="zoom:80%;" />

  2. 将原本index.js里export default复制到count.js (modules部分不用复制)

  3. index.js修改为:

     ```js
     import Vue from "vue";
     import Vuex from "vuex";
     import count from "./count"
     
     Vue.use(Vuex);
     
     export default new Vuex.Store({
       // 当 key 与 value 一样时, 可以只写一个(ES6的属性简写)
       modules: {
         count
       },
     });
     ```

  4. 在使用的时候, 不能再使用字符串的方式了, 要用箭头函数的形式

     ```js
     //如果store中count分为模块, 就不能用字符串的方式了,要用箭头函数
          count: state => state.count.count
     //state.模块名.属性
     ```

* **组合Action**

  * `store.dispatch` 可以处理被触发的 action 的处理函数返回的 Promise，并且 `store.dispatch` 仍旧返回 Promise

    ```js
    actions: {
        actionA({ commit } {
              return new Promise((resolve, reject) => {
            	setTimeout(() => {
                    commit('someMutation')
                    resolve()
                },1000)
        	  })  
        })
    }
    ```

    ```js
    store.dispatch('actionA').then(() => {
        //...
    })
    ```

    在另一个action中也可以这样用: 

    ```js
    actions: {
        //...
        actionB ({dispatch, commit}) {
            return dispatch('actionA').then(() => {
                commit('someOtherMutation')
            })
        }
    }
    ```

    利用async/await, 可以实现组合Action: 

    ```js
    // 假设 getData() 和 getOtherData() 返回的是 Promise
    actions: {
        async actionA ({ commit }) {
            commit('gotData', await getData())
        },
        async actionB({ dispatch, commit }) {
            await dispatch('actionA') //等待actionA完成
            commit('gotOtherData',await getOtherData())
        }
    }
    ```

    

### Element常用组件----布局组件

官网: [Element - 网站快速成型工具](https://element.eleme.cn/#/zh-CN)

1. 安装element-ui  

   ```js
   npm i element-ui -S
   ```

   -S指令就是全局安装, 在开发和生产环境上都安装

2. 引入和挂载到全局

   ```js
   //main.js
   import ElementUI from 'element-ui';
   import 'element-ui/lib/theme-chalk/index.css';
   
   Vue.use(ElementUI);
   ```

3. 这样就可以在任何地方使用element-ui的组件了

* 24分栏布局示例: 

  ```vue
  <template>
      <div>
          <h3>带间隔的4等分布局</h3>
          <!-- :gutter="20"  col之间的间隔为20px -->
          <el-row :gutter="20">
              <el-col :span="6"><div class="content">1</div></el-col>
              <el-col :span="6"><div class="content">2</div></el-col>
              <el-col :span="6"><div class="content">3</div></el-col>
              <el-col :span="6"><div class="content">4</div></el-col>
          </el-row>
      </div>
  </template>
  <style scoped>
  .content {
      background-color: #000;
      color: #fff;
  }
  </style>
  ```

* Container布局示例

  ```vue
  <el-container>
    <el-header>Header</el-header>
    <el-main>Main</el-main>
    <el-footer>Footer</el-footer>
  </el-container>
  ```

  

### Element常用组件----弹出类型组件

* 常用弹出插件
  * el-dialog
  * el-popover

* sync修饰符的作用--更简单地向父组件通信

  * 如何实现双向绑定? (下面的实例: 更新title的值为newTitle)

    1. 在子组件中触发updata:title事件 `this.$emit('updata:title', newTitle)`

    2. 然后在父组件中监听updata:title事件并根据需要更新一个本地的数据: 

    ```vue
    <text-document
          v-bind:title="doc.title"
          v-on:updata:title="doc.title = $event"
    </text-document>
    ```

    `.sync` 修饰符就是这种模式的一个缩写

    ```vue
    <text-document v-bind:title.sync="doc.title"></text-document>
    ```

    当需要用一个对象同时设置多个prop是, 可将`.sync`和`v-bind`结合使用

    ```vue
    <text-document v-bind.sync="doc"></text-document>
    ```

    这样会把`doc`对象中的每一个property(如`ttile`)都作为一个独立的prop穿进去,然后各自添加用于更新的`v-on`监听器

  * 示例: ElementUI中的el-dialog

    ```js
    //写法一
    <el-dialog :visible.sync="dialogVisible">
    //通过sync实现数据绑定. 在点击空白处时el-dialog组件内会修改当前值状态,通过sync修饰符传递给父组件,实现关闭dialog
    
    //写法二
    <el-dialog :visible="dialogVisible" :before-close="handleClose">
    methods: {
        handleClose(done) {
          this.$confirm("确认关闭？")
            .then((_) => {
              //关闭弹出框
              this.dialogVisible = false
              done();
            })
            .catch((_) => {});
        }
      },
    ```

  * el-dialog的插槽

    

* popover

  

### Element常用组件----表格组件

* 基础表格

* 表格常用属性

  | 属性名         | 作用                                                   |
  | -------------- | ------------------------------------------------------ |
  | height         | 给表格设置高度, 同时固定表头                           |
  | show-header    | 设置是否显示表头                                       |
  | row-class-name | 设置一个函数或者固定的名字作为行的类名                 |
  | border         | 是否显示表格竖直方向的边框, 设置后通过改变边框设置列宽 |

* 列常用属性

  | 属性名                | 作用                                   |
  | --------------------- | -------------------------------------- |
  | label                 | 当前列的表头名称                       |
  | prop                  | 传入的表格json数据的key值              |
  | show-overflow-tooltip | 是否设置文字超出列宽时悬浮显示完整内容 |

  ```vue
  <template>
    <div>
      <el-table :data="tableData" style="width: 100%" height="400" border>
        <el-table-column prop="date" label="日期" width="180"> </el-table-column>
        <el-table-column prop="name" label="姓名" width="180"> </el-table-column>
        <el-table-column prop="address" label="地址"  show-overflow-tooltip> </el-table-column>
        <el-table-column label="操作">
            <!-- slot-scope将子组件中的变量绑定到当前标签上 scope是变量名,可任意更改,可利用scope调用子组件内的变量 -->
        <template slot-scope="scope">
          <el-button
            size="mini"
            @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
            <!-- scope.$index是当前行数   scope.row是当前行对象 -->
          <el-button
            size="mini"
            type="danger"
            @click="handleDelete(scope.$index, scope.row)">删除</el-button>
        </template>
      </el-table-column>
      </el-table>
    </div>
  </template>
  
  <script>
  export default {
    name: "CodeTable",
  
    data() {
        
      return {
        tableData: [
          {
            date: "2016-05-02",
            name: "王小虎",
            address: "上海市普陀区金沙江路 1518 弄",
          },
          {
            date: "2016-05-04",
            name: "王小虎",
            address: "上海市普陀区金沙江路 1517 弄",
          },
          {
            date: "2016-05-01",
            name: "王小虎",
            address: "上海市普陀区金沙江路 1519 弄",
          },
          {
            date: "2016-05-03",
            name: "王小虎",
            address: "上海市普陀区金沙江路 1516 弄",
          },
        ],
      };
    },
  
    mounted() {},
  
    methods: {
        handleEdit(index, row) {
          console.log(index, row);
        },
        handleDelete(index, row) {
          console.log(index, row);
        }
      }
  };
  </script>
  
  <style lang="scss" scoped>
  </style>
  ```

* 对table做简易封装

  ```vue
  <el-table :data="tableData">
        <el-table-column
          v-for="(val, key) in tableLabel"
          :key="key"
          :prop="key"
          :label="val"
          width="180"
        >
        </el-table-column>
        <el-table-column label="操作" v-if="isShowOperate">
        <template slot-scope="scope">
          <el-button size="mini" @click="handleEdit(scope.$index, scope.row)"
            >编辑</el-button
          >
          <el-button
            size="mini"
            type="danger"
            @click="handleDelete(scope.$index, scope.row)"
            >删除</el-button
          >
        </template>
      </el-table-column>
      </el-table>
  
  <script>
      props: {
        isShowOperate: {
            type: Boolean,
            default: true
        }
    },
        //data中增加:
        tableLabel: {
          date: "日期",
          name: "姓名",
          address: "地址",
        },
  </script>    
  ```

  

### Element常用组件----表单组件

* from支持表单验证和自定义验证规则

* 对from进行封装

  ```vue
  <template>
  <!-- 可以看到, from表单由model和label两部分组成 -->
    <div>
      <el-form ref="form" :model="form" label-width="80px">
        <el-form-item :label="item.label" v-for="(item, index) in formLabel" :key="index">
          <el-input v-model="form[item.key]" v-if="item.type === 'input'"></el-input>
          <el-select v-model="form[item.key]" placeholder="请选择活动区域" v-if="item.type === 'select'">
            <el-option v-for="(subitem, index) in item.options" :key="index" :label="subitem.label" :value="subitem.value"></el-option>
          </el-select>
          <el-date-picker v-model="form[item.key]" v-if="item.type === 'date-picker'" type="date" placeholder="选择日期" style="width:100%;"></el-date-picker>
        </el-form-item>
      </el-form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        form: {
          name: "",
          region: "",
          date1: "",
          date2: "",
          delivery: false,
          type: [],
          resource: "",
          desc: "",
        },
        formLabel: [
            {
              label: '活动名称',
              key: 'name',
              type: 'input'
            },
            {
              label: '活动区域',
              key: 'region',
              type: 'select',
              options: [
                {
                  label: '区域1',
                  value: 'shanghai'
                },
                {
                  label: '区域2',
                  value: 'beijing'
                }
              ]
            },
            {
              label: '活动时间',
              key: 'date1',
              type: 'date-picker'
            }
        ]
      };
    },
    methods: {
      onSubmit() {
        console.log("submit!");
      },
    },
  };
  </script>
  
  <style lang="scss" scoped>
  </style>
  ```

  

### 项目搭建和技术选型

创建项目 vue create vue-manage-system

<img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211011163359727.png" alt="image-20211011163359727" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211011172127069.png" alt="image-20211011172127069" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211011172143308.png" alt="image-20211011172143308" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211011172214500.png" alt="image-20211011172214500" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211011172244385.png" alt="image-20211011172244385" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211011172329024.png" alt="image-20211011172329024" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211011172356931.png" alt="image-20211011172356931" style="zoom:80%;" />

<img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211011172446469.png" alt="image-20211011172446469" style="zoom:80%;" />

* **简要介绍所选的配置项：**
  * SCSS
    * CSS预处理器的一种, 其写法与css更为接近, 并且支持一些变量, 函数 等编程语言的特性, Sass(使用缩排语法)只是SCSS的新一版本. 其他的css预处理(如stylus, less等)也都可以实现scss的功能,他们最终可实现的功能是一样的,只是各自有各自不同的实现方式
    * 当下载到 `node-sass` 的可能会卡住, 有时需要翻墙



### 配置项目的基本环境及项目目录结构总体介绍

* 项目根目录新建vue.config.js文件

  ```js
  module.exports = {
      devServer: {
          port: 9528,
          open: true
      }
  };
  ```

* 配置ESLint

  * 下载插件

    * ESLint

    * Vetur
    * Prettier - Code formatter

  * 在 `.eslintrc.js` 中配置检查规则

    ```js
    module.exports = {
      root: true,
      env: {
        node: true,
      },
      extends: ['plugin:vue/essential', 'eslint:recommended', '@vue/prettier'],
      parserOptions: {
        parser: 'babel-eslint',
      },
      rules: {
        'no-console': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
        'no-debugger': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
        'prettier/prettier': [
          'error',
          {
            semi: false, //末尾是否使用 ;
            singleQuote: true, //使用使用 ''
            printWidth: 160, //标签属性最大长度
          },
        ]
      },
    }
    ```

  * 运行  `cnpm run lint`  即可自动格式代码

* 清理项目

  * 1. App.vue

       ```js
       <template>
         <div id="app">
       
           <router-view />
         </div>
       </template>
       
       <style lang="scss">
       </style>
       
       ```

    2. router/index.js

       ```js
       import Vue from 'vue'
       import VueRouter from 'vue-router'
       
       Vue.use(VueRouter)
       
       const routes = []
       
       const router = new VueRouter({
         routes,
       })
       
       export default router
       ```

    3. 删除不必要的文件后的目录结构

       <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211011205919806.png" alt="image-20211011205919806" style="zoom:80%;" />

### 配置全局变量

* 使用加 `_` 的命名代表这是一个配置文件(或着说是内部文件), 这仅仅是一种友好的命名规范,并不是强求.

* scss中定义变量: 

  `$theme-color: #33aef0;`

  在assests/scss/_variable.scss文件中写入: `$theme-color: #33aef0;`

* 在`vue.config.js`中添加css预处理器配置: 

  ```js
  css: { 
      loaderOptions: { //预处理项
        sass: {
            // 引入一个全局文件
          data: `@import "@/assets/scss/_variable.scss";`
          // 如果是新版的sass-loader,则使用如下: 
          prependData: `@import "@/assets/scss/_variable.scss";`
        }
      }
    }
  ```
  
  `@` 符号就是告诉sass这个相对路径, 在编译时要翻译为绝对路径
  
  现在, 在任何地方都可以使用`$theme-color`变量
  
  ```vue
  <style lang="scss">
  #app {
    color: $theme-color;
  }
  </style>
  ```

* 引入项目初始化scss文件reset.scss   (在课程的资源文件中)

  ```js
  // main.js
  //todo 引入scss初始化文件  --需要加后缀.scss, 因为默认是加.js后缀
  import '@/assets/scss/reset.scss'
  ```

  

### 后台视频管理系统之公用部分---需求分析及模块划分

<img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211021151120463.png" alt="image-20211021151120463" style="zoom:80%;" />

## 之后进入项目实战, 不在详细记录没一步的操作(没必要,也繁琐,还不一定看..), 只记录关键技术点

### ElementUI全局安装并完整引入

### css新单位: vh

* vh即当前可见视图高度, 将其设为100vh即将元素高度设为占满当前可见视图.

### css样式覆盖, 引入css样式时, 如果有相同的css属性被声明,那么引入在前的会覆盖引入在后的. 

### key

* `key` 的特殊 attribute 主要用在 Vue 的虚拟 DOM 算法
* 使用 key 时，它会基于 key 的变化重新排列元素顺序，并且会移除 key 不存在的元素。
* 有相同父元素的子元素必须有**独特的 key**。重复的 key 会造成渲染错误

### scss继承写法

```scss
.el-breadcrumb__item {
  .el-breadcrumb__inner {
    // 设置面包屑字体颜色为白色, 上面的一长串css名是直接在浏览器里看的
    color: #fff;
  }
  //scss中集成上级class名,相当于: .el-breadcrumb__item:last-child
  &:last-child {
    .el-breadcrumb__inner {
      // 设置面包屑字体颜色为白色, 上面的一长串css名是直接在浏览器里看的
      color: #fff;
    }
  }
}
```

### *elementUI调整尺寸大小的属性大多是size*

### 在需要v-for和v-if搭配使用的场景下, 多使用v-for和计算属性来替代v-if

```js
computed: {
    //计算属性
    noChildren() {
      //对asideMenu进行过滤,返回asideMenu数组中没有children属性的成员
      return this.asideMenu.filter((item) => !item.children)
    },
    hasChildren() {
      //对asideMenu进行过滤,返回asideMenu数组中没有children属性的成员
      return this.asideMenu.filter((item) => item.children)
    },
  },
```

### 使用vuex实现切换tab页功能

* 在`Main.vue`中引入`CommonTab.vue`组件
* 在`vuex`里定义存取标签的`tagList`, 方便非父子传递数据
* 定义`vuex`中侧边栏点击后将菜单加入到`tagList`中的方法
* 定义`vuex`中点击标签后触发删除的方法

### 优化elementUI样式

* 如果elementUI有提供属性, 则直接通过设置属性值来更改样式
* 没有提供属性则在浏览器中查看class名, 通过设置css属性来更改样式

### axios全局配置

* 项目中新建 api/config.js

  ```js
  import axios from 'axios'
  // 创建一个axios实例
  const service = axios.create({
    //请求超时时间
    timeout: 3000,
  })
  
  // 添加请求拦截器
  service.interceptors.request.use(
    (config) => {
      return config
    },
    (err) => {
      console.log(err)
    }
  )
  //响应拦截器
  service.interceptors.response.use(
    (response) => {
      let res = {}
      // 可以做一个响应状态码判断,如果是200则返回,如果是404则跳转到404页面
      res.status = response.status
      res.data = response.data
      return res
    },
    (err) => console.log(err)
  )
  
  export default service
  
  ```

* main.js中引入,并挂载到vue实例

  ```js
  import http from '@/api/config'
  Vue.prototype.$http = http
  ```

### mock

* mock可以拦截请求并按照一定要求返回随机数据

* 在项目下新建 mock/index.js

  ```js
  import Mock from 'mockjs'
  import homeApi from './home'
  
  // 设置200-2000毫秒延时请求数据
  Mock.setup({
    timeout: '200-2000',
  })
  
  //首页相关
  //拦截的是 /home/getData  所拦截的http方法是get  拦截后执行的方法是homeApi.getHomeData
  // 正则表达式: 使用/ /包裹,转义字符是 \
  Mock.mock(/\/home\/getData/, 'get', homeApi.getHomeData)
  ```

* 在项目下新建 mock/home.js

  ```js
  import Mock from 'mockjs'
  
  export default {
    getHomeData: () => {
      return {
        code: 20000,
        data: {
          videoData: [
            {
              name: 'SpringBoot',
              value: Mock.Random.float(1000, 10000, 0, 2),
            },
            {
              name: 'Vue',
              value: Mock.Random.float(1000, 10000, 0, 2),
            },
            {
              name: '小程序',
              value: Mock.Random.float(1000, 10000, 0, 2),
            },
            {
              name: 'Docker',
              value: Mock.Random.float(1000, 10000, 0, 2),
            },
            {
              name: 'ES6',
              value: Mock.Random.float(1000, 10000, 0, 2),
            },
            {
              name: 'JS',
              value: Mock.Random.float(1000, 10000, 0, 2),
            },
          ],
        },
      }
    },
  }
  ```

* 在main.js中

  ```js
  import './mock'
  ```

* 在Home.vue中

  ```js
  mounted() {
      this.$http.get('/home/getData').then((res) => {
        console.log(res.data)
      })
    },
  ```

### 布局

* 完成漂亮的页面的第一步是完页面的框架布局, 之后再往每一块中填充内容

* elementUI提供了Layout布局方式

* flex布局非常好用

* 布局样式最好可以分写在单独的scss页面中

  * ```vue
    <style lang="scss" scoped>
    // scss引入语法, 前加@ 路径加~代表相对路径, 路径中@代表src目录
    @import '~@/assets/scss/home';
    </style>
    ```

### 绑定样式

* ```vue
  <i class="icon" :class="`el-icon-${item.icon}`" :style="{ background: item.color }"></i>
  ```

* 垂直布局

  * 传统方式

    ```scss
    text-align: center;
    line-height: 80px;
    color: #fff;
    ```

  * flex方式

    ```scss
    display: flex;
    // 设置排列方式(主轴)为垂直方向, 否则会默认水平展开
    flex-direction: column;
    // justify-content其实是主轴对齐方式
    justify-content: center;
    ```

  * 组件穿透

    ```scss
    // 组件间样式修改,只能修改el-card外层的样式,再往里就无法修改了,这是需要加 /deep/ 来穿透修改
                // 大多涉及这种情况的时候, elementUI应该用提供相应的属性来解决---比如这里就可以使用 body-style来替代
                // /deep/ .el-card__body {
                //     display: flex;
                // }
    ```

  * flex换行

    ```scss
    // 使用flex布局
            display: flex;
            // 换行--不设置的话, flex布局会默认将元素放在同一行,并重新计算元素宽度
            flex-wrap: wrap;
            // 水平上: 两端对齐--左边靠最左边,右边靠最右边,中间的均匀对齐
            justify-content: space-between;
    ```

### 读取响应数据

* 注意, 仔细观察返回的数据有几层data: 

  <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211024110347878.png" alt="image-20211024110347878" style="zoom:80%;" />

### table使用

* 定义一组表头

  ```js
  tableLabel: {
          name: '课程',
          todayBuy: '今日购买',
          monthBuy: '本月购买',
          totalBuy: '总购买',
        },
  ```

* 用v-for循环显示

  ```vue
  <el-table :data="tableData">
            <!-- v-for中, val即值, key即键 -->
            <!-- prop即接收的数据的键值名, label即表头 -->
            <el-table-column show-overflow-tooltip v-for="(val, key) in tableLabel" :key="key" :prop="key" :label="val"> </el-table-column>
          </el-table>
  ```

* show-overflow-tooltip  让数据单行显示

### echarts组件封装1

```vue
<template>
  <!-- //TODO 封装echarts组件 -->
  <!-- 之后通过ref来找到这个dom, 类似id -->
  <div style="height: 100%" ref="echart">echart</div>
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'VueManageSystemEchart',
  // 数据是由父组件传来的, 所以需要接受数据
  props: {
    chartData: {
      type: Object,
      //   通过函数返回对象, 这样就避免的其他组件对我们的影响: 为什么, 如何直接设为对象, 那么当使用的时候就会产生多个此对象的引用,任何一处发生更改都会影响到其他地方
      default() {
        return {
          // x轴
          xData: [],
          //   数据--也决定了图标样式即type
          series: [],
        }
      },
    },
    // 是否有坐标轴
    isAxisChart: {
      type: Boolean,
      default: true,
    },
  },
  computed: {
    //   通过判断父组件传来的isAxisChart来决定使用哪组数据格式(有坐标轴,无坐标轴)
    options() {
      return this.isAxisChart ? this.axisOption : this.normalOption
    },
  },
  data() {
    return {
      // echart对象容器,因为官网指明了,必须先初始化一个echart对象,再将数据填入容器
      echart: null,
      //   echart大致分两种: 有坐标轴图表和无坐标轴图标
      axisOption: {},
      normalOption: {},
    }
  },

  mounted() {},

  methods: {
    //初始化图表
    initChart() {
      // 如果echart对象已经存在则直接渲染图表
      if (this.echart) {
        this.echart.setOption(this.options)
      } else {
        //   如果echart对象不存在则先初始化再渲染图表
        this.echart = echarts.init(this.$refs.echart)
        this.echart.setOption(this.options)
      }
    },
    // 处理图表数据 --依据有无坐标轴分别处理
    initChartData() {
      if (this.isAxisChart) {
        console.log('axis')
      } else {
        console.log('normal')
      }
    },
  },
}
</script>

<style lang="scss" scoped></style>

```

### echarts组件封装2

```vue
<template>
  <!-- //TODO 封装echarts组件 -->
  <!-- 之后通过ref来找到这个dom, 类似id -->
  <div style="height: 100%" ref="echart">echart</div>
</template>

<script>
//todo 引入echarts  ---注意: 引入方式和以前不一样了
import * as echarts from 'echarts'
export default {
  name: 'VueManageSystemEchart',
  // 数据是由父组件传来的, 所以需要接受数据
  props: {
    chartData: {
      type: Object,
      //   通过函数返回对象, 这样就避免的其他组件对我们的影响: 为什么, 如何直接设为对象, 那么当使用的时候就会产生多个此对象的引用,任何一处发生更改都会影响到其他地方
      default() {
        return {
          // x轴  --因为y轴数据只需要一个值,这个值来自series,所以y轴不需要额外的处理
          xData: [],
          //   数据--也决定了图标样式即type
          series: [],
        }
      },
    },
    // 是否有坐标轴
    isAxisChart: {
      type: Boolean,
      default: true,
    },
  },
  computed: {
    //   通过判断父组件传来的isAxisChart来决定使用哪组数据格式(有坐标轴,无坐标轴)
    options() {
      return this.isAxisChart ? this.axisOption : this.normalOption
    },
  },
  //   监听  --这里监听复杂数据类型,需要开启deep
  watch: {
    //   当chartData(父组件传来的)发生变化时渲染图表
    chartData: {
      handler: function () {
        this.initChart()
      },
      deep: true,
    },
  },
  data() {
    return {
      // echart对象容器,因为官网指明了,必须先初始化一个echart对象,再将数据填入容器
      echart: null,
      //   echart大致分两种: 有坐标轴图表和无坐标轴图标
      axisOption: {
        // 图例 --即图表上面内容
        legend: {
          textStyle: {
            color: '#333',
          },
        },
        // 位置偏移
        grid: {
          left: '20%',
        },
        // 悬浮提示
        tooltip: {
          // 触发时机---当鼠标在坐标轴范围内时
          trigger: 'axis',
        },
        xAxis: {
          type: 'category',
          data: [],
          //   轴线设置
          axisLine: {
            //   轴线样式
            lineStyle: {
              // 轴线颜色
              color: '#17b3a3',
            },
          },
          //   标签(文本)颜色
          axisLabel: {
            color: '#333',
          },
        },
        yAxis: {
          type: 'value',
          axisLine: {
            lineStyle: {
              color: '#17b3a3',
            },
          },
        },
        // 主题色
        color: [
          '#2ec7c9',
          '#b6a2de',
          '#5ab1ef',
          '#ffb980',
          '#d87a80',
          '#8d98b3',
          '#e5cf0d',
          '#97b552',
          '#95706d',
          '#dc69aa',
          '#07a2a4',
          '#9a7fd1',
          '#588dd5',
          '#f5994e',
          '#c05050',
          '#59678c',
          '#c9ab00',
          '#7eb00a',
          '#6f5553',
          '#c14089',
        ],
        series: [],
      },
      normalOption: {
        legend: {
          show: false,
        },
        tooltip: {
          // 触发时机---鼠标在数据项上时
          trigger: 'item',
        },
        color: ['#0f78f4', '#dd536b', '#9462e5', '#a6a6a6', '#e1bb22', '#39c362', '#3ed1cf'],
        series: [],
      },
    }
  },

  mounted() {},

  methods: {
    //初始化图表
    initChart() {
      // 渲染数据
      this.initChartData()
      // 如果echart对象已经存在则直接渲染图表
      if (this.echart) {
        this.echart.setOption(this.options)
      } else {
        //   如果echart对象不存在则先初始化再渲染图表
        this.echart = echarts.init(this.$refs.echart)
        this.echart.setOption(this.options)
      }
    },
    // 处理图表数据 --依据有无坐标轴分别处理
    initChartData() {
      //   将父组件传来的数据存进data
      if (this.isAxisChart) {
        // 使用有坐标轴的数据属性
        this.axisOption.xAxis.data = this.chartData.xData
        this.axisOption.series = this.chartData.series
      } else {
        // 使用无坐标轴的数据属性
        this.normalOption.series = this.chartData.series
      }
    },
  },
}
</script>

<style lang="scss" scoped></style>

```

* 当需要isAxisChart为false时(即使用不带坐标轴的图表), 需要为此子组件传入值: 

  ```vue
  <echart style="height: 260px" :chartData="echartData.video" :isAxisChart="false"></echart>
  ```

  

### EChart组件封装总结

* 观察echart官方文档， 先考虑组件需要的基本参数

  <img src="https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211101135814372.png" alt="image-20211101135814372" style="zoom: 67%;" />

* 对参数进行筛选， 哪些参数需要从父组件传来， 哪些参数是组件自身的参数

  可以看到, 首先, `title`应该从父组件传来, `悬浮提示`可以是自身参数, `图例`与`series的name`一般保持一致(所以可以是自身), `x轴数据`应该从父组件传来, `y轴数据`相对简单(可以不多考虑), `图表的数据`当然需要父组件传, 

* 完善组件，参照设计图, 找不同的地方, 再到echart文档里寻找对应的配置项

* 细节优化, 考虑多种场景下, 图标自适应的处理

  ```js
  //重新计算图表大小
  this.echart.resize()
  
  
  // 监听到resize事件时执行resizeChart
      window.addEventListener('resize', this.resizeChart)
      // 当浏览器窗口被调整到一个新的高度或宽度时，就会触发resize事件。
  ```

  

### 页面划分

![image-20211101144538155](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211101144538155.png)

这样的底部条, 可以是一个form, 封装成我们的一个组件

![image-20211101144614997](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211101144614997.png)

这样的表格和分页, 可以封装进一个组件



### 权限管理思路

* 权限管理
  * 根据不同用户, 返回不同菜单
  * 严格控制用户权限
  * 实现思路
    * 动态路由
    * 后端返回的数据格式要求(返回基本的路由配置参数, url要是字符串,前端完成拼接)
    * 触发时机
      * 登录成功的时候触发操作

* 权限管理之动态返回菜单的实现

  * 更改路由表
    * 根据是否需要权限的路由分类(对于需要权限的路由则动态生成, 不需要的则直接前端写死)

  * vuex里补充mutation
    * 保存菜单
    * 动态添加菜单

  * 生成路由的时机
    * 登录时:  在login页面跳转home前
    * 刷新时:  在main.js中, 初始化vue时
    * 还有一些小问题, 在路由拦截中应该清空vuex中的一些数据,比如面包屑

### 操作cookie需要使用`npm i js-cookie`

### 权限管理之路由守卫判断用户登录状态

* `permission.js`中返回token(返回menu的同时也返回token)
* 登录时保存token
  * 保存在vuex里
  * 保存在cookie里

* 路由守卫根据判断token存在与否, 判断用户页面跳转

* *<!-- //TODO 本组件并未定义click事件,这里使用.native修饰符表示使用vue原生的click事件 -->*

  ​     `<el-dropdown-item @click.native="logOut">退出</el-dropdown-item>`

* 刷新浏览器

  ```js
  // 刷新浏览器
        location.reload()
  ```

  

### 项目总结

* 退出登录后要刷新页面, 因为我们项目中登录时已经将路由添加进router, 如果不刷新,router不会更新(刷新页面时我们设置了构造函数, 重新获取路由)

* 项目当中遇到坑,如何解决: 
  * 通过`vue-devtool`调试
  * 通过console输出调试, 点击报错信息跳转到源码, 利用console输出报错的位置

* 组件的封装思路

  * 判断基本参数
    * 哪些可以写死在组件里
    * 哪些是需要父组件传来

  * 扩展
    * 自定义事件, 判断传出哪些参数
    * 插槽拓展

  * 优化
    * 提供组件的适应性(包括样式, 大小, 多种情况下的适应)
      * `v-if`, `v-else`, 根据父组件传入的条件来生成对应的模板

* 学习一个新技术
  * EChart
    * 要先由大局观, 直接看快速教程, 快速了解技术的基础构成(知道基础结构了就可以尝试封装了)
    * 分成几部分, 在对应部分查找文档
