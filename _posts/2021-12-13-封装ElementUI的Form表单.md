---
layout: post
title: '封装ElementUI的Form表单'
subtitle: '更高效地使用饿了么Form表单'
date: 2021-12-13
categories: 技术
author: lalala
cover: ''
tags: server
---



### 封装ElementUI的Form表单

* CommonForm.vue   组件

  ```vue
  <template>
    <!-- 表单封装 -->
    <el-form ref="form" class="myForm" :inline="inline" :model="form" label-width="100px">
      <el-form-item
        v-for="item in formLabel"
        :key="item.model"
        :class="[{ notInline: !inline }, '']"
        :label="item.label"
      >
        <!-- 动态绑定v-model  大部分的type都是input, 那就: 如果为设置type属性,就将其显示为input,设置了type,就显示为对应的type -->
        <el-input
          v-if="!item.type || item.type === 'textarea'"
          v-model="form[item.model]"
          :style="[maxWidth, fromStyle, item.itemStyle]"
          :type="item.type"
          :placeholder="item.placeholder"
        />
        <!-- 对于select类型, 还需要配置其option, 直接在父组件中配置通过formLabel一起传来 -->
        <el-select
          v-if="item.type === 'select'"
          v-model="form[item.model]"
          :clearable="item.clearable"
          :style="[maxWidth, fromStyle, item.itemStyle]"
          :placeholder="item.placeholder"
        >
          <el-option v-for="item in item.opts" :key="item.value" :label="item.label" :value="item.value" />
        </el-select>
        <!-- 一个开关类型 -->
        <el-switch v-if="item.type === 'switch'" v-model="form[item.model]" />
        <!-- 一个单选框 -->
        <el-radio-group
          v-if="item.type === 'radio'"
          v-model="form[item.model]"
          :style="[maxWidth, fromStyle, item.itemStyle]"
        >
          <el-radio-button
            v-for="item in item.rads"
            :key="item.label"
            :class="[{radioTwo: radioRadNum === 2},{radioThree: radioRadNum === 3},{radioFour:radioRadNum === 4},'']"
            :label="item.label"
          />
        </el-radio-group>
      </el-form-item>
      <!-- 在末尾预留一个插槽 -->
      <el-form-item>
        <slot />
      </el-form-item>
    </el-form>
  </template>
  
  <script>
  export default {
    name: 'VueManageSystemCommonform',
    props: {
      // 表单列表项的通用样式
      fromStyle: Object,
      // 是否显示为行即表单
      inline: Boolean,
      // 表单值（v-model双向绑定）
      form: Object,
      // 表单项配置 --每一项都是一个对象例如: { model: 'keyword',label: '', type: 'select', ops:[ {value: '', label: ''} ] }
      formLabel: Array
    },
    data() {
      return {
        radioTwo: 'radioTwo',
        radioThree: 'radioThree',
        radioFour: 'radioFour',
        notInline: 'notInline',
        // 默认单项的最大宽度
        maxWidth: {
          maxWidth: '180px'
        }
      }
    },
    computed: {
      // 如果传来的formLabel中有radio类型,那么就计算该项里rads的项的个数
      radioRadNum() {
        const number = this.formLabel.find(item =>
          item.type === 'radio'
        ).rads.length || 0
        // console.log(number)
        return number
      }
    },
  
    mounted() {},
  
    methods: {}
  }
  </script>
  
  <style lang="scss" scoped>
  	.el-form-item {
  		margin-bottom: 0;
  	}
  
  	.el-form :last-child {
  		margin-right: 0;
  	}
  
  	.el-form-item {
  		margin-bottom: 0;
  	}
  
  	.el-form :last-child {
  		margin-right: 0;
  	}
  
  	.notInline {
  		margin-bottom: 20px;
  	}
  </style>
  <style lang="scss">
  	// 定义两个数组  因为需要更改el-radio-button编译后的属性,所以不能再把css作用域定在当前了
  	$widths: 50%,
  	33.3%,
  	25%;
  	$radioNum: 'Two',
  	'Three',
  	'Four';
  
  	// 循环 1-3
  	@for $i from 1 through 3 {
  
  		// 解析数组生成css
  		.radio#{nth($radioNum, $i)} {
  			width: nth($widths, $i);
  
  			.el-radio-button__inner {
  				width: 100%;
  			}
  		}
  	}
  
  	// form中label和input的间隔
  	.myForm {
  		.el-form-item__label {
  			padding-right: 24px;
  		}
  	}
  </style>
  
  ```

* 使用: 

  ```vue
  <template>
  	<common-form inline :form-label="formLabel" :form="searchFrom">
          <el-button class="normal-btn my_btn" type="primary" @click="search">搜索</el-button>
          <!-- <div class="btn">搜索</div> -->
        </common-form>
  </template>
  <script>
  import CommonForm from '@/components/Form/CommonForm.vue'
  export default {
      data() {
      	return {
          	searchFrom: {
          		keyword: '',
          		useStatus: '',
          		useType: ''
        		},
              // 表单项的通过属性--设置后将对所有表单项生效--不设置仅默认maxWidth为180px
        		fromStyle: {
          		maxWidth: '180px'
        		},
              formLabel: [
          		{
            			model: 'useStatus',
            			label: '',
            			type: 'select',
            			clearable: true,
            			placeholder: '请选择状态',
                       itemStyle: {},
            			opts: [
              			{
                				value: '0',
                				label: '禁用'
              			},
              			{
                				value: '1',
                				label: '启用'
              			}
            			]
          		},
          		{
            			model: 'useType',
            			label: '',
            			type: 'select',
            			placeholder: '请选择类型',
            			// 是否支持清空
            			clearable: true,
            			opts: [
              			{
                				value: '0',
                				label: '行政人员'
              			},
              			{
                				value: '1',
                				label: '管理人员'
              			}
            			]
          		},
          		{
            			model: 'keyword',
            			label: '',
            			placeholder: '请输入关键词'
          		}
        		],
      	}
      }
  }
  </script>    
  ```
  
  