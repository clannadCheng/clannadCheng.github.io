# 官方文档

https://segmentfault.com/a/1190000016434836 

https://www.cnblogs.com/chenhuichao/p/10818396.html

//原理思路

https://cn.vuejs.org/
https://avue.top/#/component/crud
https://avuejs.com/doc/crud/crud-menu
https://avuejs.com/doc/login

# 组件库

https://element.eleme.cn/#/zh-CN/component/form



# 安装vue脚本库
npm install -g @vue/cli



# package.json 语法
//"pvue": "2.0.0",>>指定版本 "pvue": "^2.0.0", 取高版本


# 应用语法
## Vue 对象别名 vm.$date.name = vm.data

## `new Vue({})` 创建Vue组件
var vm = new Vue({

## el 元素 指定元素id
el: '#example-2',

## 在 data 定义属性 
  // 定义 vm Vue对象的属性 vm.name == 'vue.js' 
  // vm.name='example2' 修改对象的属性值
  // vm.name='example2' 属性值相应式只支持在对象中定义的属性
  data: {
    name: 'Vue.js'
  },

## 在 `methods` 对象中定义方法(函数:函数体)
  methods: {
    greet: function (event) {
      alert('Hello ');
    }
  }
})

## Vue 自带方法
### Object.freeze() 阻止属性相应式 
### vm.$watch 监控属性变化
vm.$watch('name' function(newVal,oldVal){
    console.log(newVal,oldVal);
})


## 文本插值 {{}}

## javascript 表达式
```
{{ number + 1 }} //运算表达式
{{ ok ? 'YES' : 'NO' }} //三元表达式
{{ message.split('').reverse().join('') }}
<div v-bind:id="'list-' + id"></div>
```

## 指令
### 不更新插值  v-once
`<span v-once>{{html}}</span>`

### 文本转html代码 v-html
`<p v-html> {{html}} </p>`

### html标签绑定属性 v-bind
 v-bind:属性名=属性值(Vue组件的属性名)
`<div v-bind:class='classn'>`

### 动态参数
`<a v-bind:[attributeName]="url"> ... </a>`

### class与style绑定
```
<div v-bind:class="{ active: isActive }"></div>
<div v-bind:class="[ active ? isActive : '']"></div>
```

### 绑定内联元素
```
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```

### 条件渲染
`v-if、v-show`

### 列表渲染 index key value
```
<div v-for="(value, name, index) in object">
  {{ index }}. {{ name }}: {{ value }}
</div>
```

### 事件处理
`v-on:click="counter += 1`
#### methods 
```  
methods: {
    greet: function (event) {
      // `this` 在方法里指向当前 Vue 实例
      alert('Hello ' + this.name + '!')
      // `event` 是原生 DOM 事件
      if (event) {
        alert(event.target.tagName)
      }
    }
  }
 // 也可以用 JavaScript 直接调用方法
vm.greet() // => 'Hello Vue.js!' 
```

### 表单输入绑定 v-model
```
<input v-model="message" placeholder="edit me">
<p>Message is: {{ message }}</p>
```

## 组件基础 chapter12
```
Vue.component('button-counter', {
	props: ['title'],
	data: function () {
		return {
		  count: 0
		}
	},
	template: '<div><h1>hi...</h1><button v-on:click="clickfun">{{title}} You clicked me {{ count }} times.</button><slot></slot></div>',
	methods:{
		clickfun : function () {
			this.count ++;
			this.$emit('clicknow', this.count);
		}
	}
})
```

## 组件注册 chapter13 components
```
var vm = new Vue({
	el : "#app",
	data : {
		
	},
	methods:{
		clicknow : function (e) {
			console.log(e);
		}
	},
  //组件
	components:{
		test : {
			template:"<h2>h2...</h2>"
		}
	}
});
```

## Vue生命周期钩子




