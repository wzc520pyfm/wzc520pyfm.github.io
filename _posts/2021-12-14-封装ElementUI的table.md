---
layout: post
title: '封装ElementUI的table'
subtitle: '更高效地使用饿了么table'
date: 2021-12-14
categories: 技术
author: lalala
cover: ''
tags: 前端
---



### 封装ElementUI的table

* CommonTable.vue  组件

  ```vue
  <template>
    <div class="common-table">
      <!-- stripe 斑马纹  高度设为百分比,将会继承外层div即common-table的高度 v-loading即显示局部加载 -->
      <el-table
        v-loading="config.loading"
        highlight-current-row
        :header-cell-style="config.headerCellStyle"
        :border="config.border"
        :data="tableData"
        stripe
        :max-height="viewHeight"
        @sort-change="handleSortChange"
        @selection-change="handleSelectionChange"
      >
        <el-table-column
          v-if="config.selection"
          :align="config.align"
          :fixed="config.selFixed"
          type="selection"
          width="55"
        />
        <!-- 因为序号是大多数表格都有的, 所以直接单独设置一个column -->
        <el-table-column
          :align="config.align"
          :fixed="config.numFixed"
          label="序号"
          width="85"
        >
          <!-- scope是插槽作用域,通过它可以在插槽内访问到table内的数据,比如row,column,$index,store(table内部的状态管理)等 -->
          <template slot-scope="scope">
            <!-- 序号, 分页的当前第几页(第一页不算故减一)*每页的项数 + 当前列表序号(从0开始) + 1 -->
            <span style="margin-left: 10px">{{
              (config.page - 1) * config.pageSize + scope.$index + 1
            }}</span>
          </template>
        </el-table-column>
  
        <el-table-column
          v-for="item in tableLabel"
          :key="item.prop"
          show-overflow-tooltip
          :label="item.label"
          :prop="item.prop"
          :align="config.align"
          :fixed="item.fixed"
          :sortable="item.sortable"
          :min-width="item.width ? item.width : '180px'"
        >
          <template slot-scope="scope">
            <!-- scope.row[item.prop] 将会显示该prop对应的label  如果获取到的数据不完整,就可能会导致scope.row[item.prop]为空,这必然会导致table渲染出错(报错:无法解析null),解决方法很简单,只要判断scope.row[item.prop]是否为空,当其不为空时才渲染数据,为空则舍弃 -->
            <span
              v-if="!item.type && scope.row[item.prop]"
              style="margin-left: 10px"
            >{{
              scope.row[item.prop] | valueFilter(scope.row[item.prop].filter)
            }}</span>
            <slot v-if="item.type === 'button'" :scope="scope" />
          </template>
        </el-table-column>
      </el-table>
      <!-- //todo 在组件内部操作分页后需要同步到父组件, 通过sync操作符即可实现双向绑定数据 -->
      <el-pagination
        class="pager"
        layout="total, sizes, prev, pager, next, jumper"
        :page-sizes="config.pageSizes"
        :page-size="config.pageSize"
        :total="config.total"
        :current-page.sync="config.page"
        @size-change="handleSizeChange"
        @current-change="changePage"
      />
    </div>
  </template>
  
  <script>
  export default {
    name: 'VueManageSystemCommontable',
    filters: {
      valueFilter: function(value, arr) {
        if (!arr) return value
        // console.log(value)
        // todo 如果arr[0].text是number, 则执行下面的过滤操作, 如果是正则表达式(字符串),则执行正则匹配(原本的值仍保存在.label内)
        if (typeof arr[0].text === 'number') {
          // console.log("number",arr[0].text)
          for (const item of arr) {
            if (value.label === item.text) {
              return item.value
            }
          }
        } else if (typeof arr[0].text === 'string') {
          let myReg = new RegExp(arr[0].text)
          let resultArray = myReg.exec(value.label)
          let newStr = arr[0].value
          //! 1.padEnd是异步的  2.当保错无法读取null时,估计是数据异常了,增加空值处理即可(参照下方处理方式)
          return value.label && resultArray
            ? value.label.replace(
              resultArray,
              newStr.padEnd(resultArray.index, arr[0].value)
            )
            : value.label
        }
  
        return '过滤出错'
      }
    },
    props: {
      tableData: Array,
      tableLabel: Array,
      // 接收表格的其他配置, 如列宽,是否显示加载中, 分页参数等
      config: Object
    },
    data() {
      return {
        height: 100
      }
    },
    computed: {
      viewHeight() {
        let height = this.config.maxHeight || '63vh'
        // console.log(this.config.height)
        var parts = height.match(/([0-9\.]+)(vh|vw)/)
        var q = Number(parts[1])
        var side =
          window[['innerHeight', 'innerWidth'][['vh', 'vw'].indexOf(parts[2])]]
        return side * (q / 100)
      }
    },
    created() {
      // this.height = this.viewHeight(this.config.height);
      // this.height = this.viewHeight();
      // console.log(this.height)
    },
    mounted() {},
  
    methods: {
  
      changePage(page) {
        // page将作为参数传给父组件的监听回调函数
        this.$emit('changePage', page)
      },
      // '每页多少项' 更新
      handleSizeChange(size) {
        this.config.pageSize = size
        this.$emit('changePage', size)
      },
      // 当表格的排序条件发生变化时会触发该事件
      handleSortChange({ column, prop, order }) {
        this.$emit('handleSortChange', column, prop, order)
      },
      // 选择项发生变化时触发
      handleSelectionChange(val) {
        this.$emit('selection-change', val)
      }
    }
  }
  </script>
  
  <style lang="scss" scoped>
  .common-table {
    // 计算, 高度设为100%减去顶部header的部分
    //   height: calc(100% - 80px);
    background-color: #fff;
    .pager {
      // position: absolute;
      margin-top: 20px;
      text-align: center;
    }
  }
  </style>
  
  ```

* 使用: 

  ```vue
  <template>
  	<common-table
        :table-data="tableData"
        :table-label="tableLabel"
        :config="config"
        @changePage="getList"
        @handleSortChange="handleSortChange"
        @selection-change="handleSelectionChange"
      >
        <template #default="{ scope }">
          <!-- row就是行的数据  scope是table内部定义的变量-->
          <el-button
            size="mini"
            type="text"
            @click="editAcc(scope.row)"
          >编辑</el-button>
          <el-button
            size="mini"
            type="text"
            @click="handleBan(scope.row)"
          >禁用</el-button>
        </template>
      </common-table>
  </template>
  <script>
  import CommonTable from '@/components/Tables/CommonTable.vue'
  export default {
    name: 'HealthBG',
    components: { CommonTable },
    data() {
      return {
          tableData: [],
          // 在组件中通过循环tableLabel即可生成表格
        tableLabel: [
          {
            prop: 'type',
            label: '类型'
          },
          {
            prop: 'username',
            label: '用户名'
          },
          {
            prop: 'name',
            label: '姓名'
          },
          {
            prop: 'phone',
            label: '电话号码',
            // 是否支持排序--值为 'custom'代表开启后端排序, 需要在common-table标签中监听handleSortChange事件
            sortable: 'custom'
          },
          // {
          //   prop: 'password',
          //   label: '密码'
          // },
          {
            prop: 'status',
            label: '状态',
            filter: [
              {
                text: '',
                value: ''
              }
            ]
          },
          {
            prop: 'operate',
            label: '操作',
            type: 'button',
            fixed: 'right'
          }
        ],
        config: {
          // 表格是否显示选择框
          selection: true,
          // 选择框列是否固定
          selFixed: true,
          // 表格的序号列是否固定
          numFixed: true,
          // 表格是否显示表格线
          border: true,
          // 表格最大高度 --不设置则默认70vh
          maxHeight: '70vh',
          // 表头样式
          headerCellStyle: {
            background: '#F0F5FF'
          },
          // 表格内容对齐方式
          align: 'center',
          // 当前是第几页
          page: 1,
          // 总计有多少页
          total: -1,
          // 一页多少项
          pageSize: 5,
          // 可供选择的 '一页多少项'
          pageSizes: [20, 50, 100, 150],
          // 是否加载中
          loading: false,
          // 表格当前的排序方式
          order: '',
          // 表格当前排序列的prop
          orderProp: ''
        },
      }
    },
    methods: {
        // 后端排序回调函数 ---column是一个对象(当前列的对象), prop是当前列的prop, order是排序方式(字符串,默认排序时其值为null)
      handleSortChange(column, prop, order) {
        console.log('column', column, 'prop', prop, 'order', order)
        this.config.order = order === null ? '' : order === 'ascending' ? 'asc' : 'desc'
        this.config.orderProp = prop === 'phone' ? 'sysUserPhone' : ''
        // 重新请求后端数据
        this.getList()
      },
        //表格选择项改变时触发
      handleSelectionChange(val) {
        console.log(val)
      }
    }
  }
  </script>    
  ```

  