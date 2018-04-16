# vue
vue基础知识
# vue核心思想
```
M : Model 模型/数据
V : View 视图
VM : View-Model 视图模型

MVVM要解决的问题:
	视图和模型分离的问题
  
 ```
  
 # vue基本指令
 ```
 ## 作用:
	  操作dom,View-Model就是利用这些指令,将数据填充到View
	  上面去展示的
	
  注意点:
	  我们在Vue中,大部分情况下,我们不要再直接操作dom了,应该操作Vue中的数据,
	  当数据改变了,Vue会使用它内部的指令去操作dom,进行渲染
  
 ```
 ```
 ## 基本指令
 {{}}:
   插值表达式 
 
v-text:
	这个是插值表达式的另外一种写法
	注意:不能放到文本框中使用,通常是放到 div span p 标签中使用
	
v-html:
	这个能保证字符串中的html标签也能被浏览器正常解析
	
v-on:
	给html元素注册一些js事件:
		click事件,change事件,keyup,keydown,xxx
		
	写法:
		在html元素中 <button v-on:click="click">显示或是隐藏元素</button>
		
		在<script>标签中,要单独写一个 methods的代码块
		
	注意:
		可以利用@来简化html中v-on的写法
	
v-bind:
	作用:是可以在html元素上拓展任何属性,例如
	<span v-bind:title='可以是data中的一个变量'></span>
	
	利用:可以用来简写,比如<span :title='可以是data中的一个变量'></span>
	应用场景:一般动态的值需要绑定,比如img的src属性,或是需要动态变化的样式
	
	注意点:
		v-bind的特殊写法,原因是在绑定某些特殊属性的时候,这些属性由固定的字符串加上一个变量来组成,那么这个时候,如果使用 :href='getnews'+id,那么id是找不到的,应该这样写 v-bind="{href:'getnews/'+id}"
	
v-model:
	mvvm设计模式
	双向数据绑定
	使用场景:一般用在文本框中用来进行视图和模型的双向绑定
	
v-if:
	根据一个表达式的值判断,如果值为真,就解析这个html元素,否则不解析这个html元素,在原有的位置使用<!-- -->占位,注意:它不会解析
	
v-show:
	根据一个表达式的值判断,如果值为真,就显示这个html元素,否则隐藏这个html元素,注意:它会解析,注意与v-if的区别
 
```
## v-for
```
作用:
	遍历数组或者对象中的成员按照一定的模版内容重复生成html内容

遍历数组
	如:
		var list = [1,2,3];
		
	1.不需要索引
		v-for="item in list" :key="item.一个唯一标识";
	
	2.需要索引
		v-for="(item,index) in list" :key="index";
   
```
```
遍历对象中的属性
	var user={"name":"duanzihuang","age":20};
	v-for="(item,key,index) in user :key="index" ";

直接遍历整数
	v-for="item in 3" ===> 1,2,3
	
注意点:
	v-for 标签一定要加在被遍历的元素上,不要写错地方啦

```
## 自定义过滤器

```
vue1.x和2.x的区别:
	vue1.x提供了一些全局的过滤器,2.x废弃了,需要程序员自己写
```
```
组件私有过滤器:
	定义:
		在组件的<script>中添加一个属性 filters:{
			tolowercase(input){
				return input.toLowerCase();
			}
		}
		
	使用:
		在组件的<template>标签中,使用的地方使用即可,例如
			{{msg | tolowercase}}
			
	不足之处:
		只能在自己定义的Vue对象中使用,在其它Vue对象中就使用不了了

全局的过滤器:
	定义:
		在main.js中定义即可
			```
				Vue.filter('toUpperCase',function(input){
				    return input.toUpperCase();
				});
			```
			
	使用:
		在组件的<template>标签中,使用的地方使用即可,例如
			{{msg | tolowercase}}
			
	注意点:
		全局过滤器的设置,一定要在创建Vue对象之前,否则不起作用
	
注意点:
  如果一个vue组件中,定义的私有过滤器的名称和全局过滤器的名称相同的化,私有过滤器的调用优先级高于全局过滤器

```
```
私有过滤器
<body>
        <div id="app1">
                <!-- 写法1 -->
                <!-- {{msg1 | toLC(msg1)}} -->

                <!-- 写法2 -->

                {{msg1 | toLC}}
        </div>

         <div id="app2">
                {{msg2 | toLC2}}
        </div>
</body>
<script type="text/javascript">
          var vm1 = new Vue({
                el:"#app1",
                data:{
                    msg1:"I AM GOOD MAN"
                },
                filters:{
                    toLC(input){
                        return input.toLowerCase();
                    }
                }
          });

          var vm2 = new Vue({
            el:'#app2',
            data:{
              msg2:"YOU ARE A GOOD Girl"
            },
            filters:{
                toLC2(input){
                    return input.toLowerCase();
                }
            }
          })
</script>
```
```
全局过滤器
<body>
        <div id="app1">
                <!-- 写法1 -->
                <!-- {{msg1 | toLC(msg1)}} -->

                <!-- 写法2 -->

                {{msg1 | toLc}}
        </div>

         <div id="app2">
                {{msg2 | toLc}}
        </div>
</body>
<script type="text/javascript">
         Vue.filter('toLc',(input)=>{
              return input.toLowerCase();
         });

          var vm1 = new Vue({
                el:"#app1",
                data:{
                    msg1:"I AM GOOD MAN"
                }
          });

          var vm2 = new Vue({
            el:'#app2',
            data:{
              msg2:"YOU ARE A GOOD Girl"
            }
          })
</script>
```
## 组件
```
作用:
	用来显示页面内容的


注意点:
	在vue2.0中,组件必须要有一个根元素
  
```
```
写法1:
<body>
        <div id="app">
                <!-- 3.使用组件 -->
               <account></account>
        </div>
</body>
<script type="text/javascript">
      //写法1
      //1.先定义
      var account = Vue.extend({
          template:'<div><a href="#">登录</a><a href="#">注册</a></div>'
      })

      //2.再注册
      Vue.component('account',account);

      new Vue({
          el:'#app'
      })
</script>
```
```
写法2：
<body>
        <div id="app">
                <!-- 3.使用组件 -->
               <account2></account2>
        </div>
</body>
<script type="text/javascript">

      //写法2
      //定义+注册
      Vue.component('account2',{
           template:'<div><a href="#">登录1</a><a href="#">注册1</a></div>'
      })

      new Vue({
          el:'#app'
      })
</script>

```
```
写法3：
<body>
        <template id="account31">
              <h1>
                <a href="#">登录31</a><br/>
        
                <a href="#">注册31</a>
              </h1>
        </template>

        <div id="app">
                <!-- 3. 使用组件 -->
               <account31></account31>
        </div>
</body>
<script type="text/javascript">
      //写法31
      Vue.component('account31',{
           template:'#account31'
      })

      new Vue({
          el:'#app'
      })
</script>

```
```
写法4:
<body>

        <div id="app">
                <!-- 使用组件 -->
                <template>
                    <h1>
                      <a href="#">登录32</a><br/>
              
                      <a href="#">注册32</a>
                    </h1>
              </template>
        </div>
</body>
<script type="text/javascript">

      new Vue({
          el:'#app'
      })
</script>

```
```
写法5：
<body>
        <!-- 步骤1 -->
        <script type="x-template" id="account4">
                <h1>
                      <a href="#">登录4</a>
                      <a href="#">注册4</a>
                </h1>
        </script>

        <div id="app">
                <!-- 步骤3.使用组件 -->
                <account4></account4>
        </div>
</body>
<script type="text/javascript">
      //写法4
      //步骤2
      Vue.component('account4',{
           template:'#account4'
      })

      new Vue({
          el:'#app'
      })
</script>
```
## vue-router
```
作用:路由跳转

网址:
	https://router.vuejs.org/zh-cn/
	https://github.com/vuejs/vue-router
	
使用:
	看文档
	见代码
	
注意点:
	1.x和2.x是不一样的
```
```
注：noparams
<body>
      <div id="app">
              <router-link to='/login'>登录</router-link>
              <router-link to='/register/rose'>注册</router-link>

              <router-view></router-view>
      </div>
</body>
<script type="text/javascript">
        //我们这个时候的组件只需要定义不需要注册，路由接管了注册的功能
        //定义登录组件
        var loginComponent = Vue.extend({
            template:'<h2>登录组件的内容</h2>'
        });

        //定义注册组件 --- 定义组件的简写方式
        var registerComponent = {
            template:'<h5>register component content  --- {{uname}}</h5>',
            //组件中的data是一个方法,并且这个方法要返回一个对象,这个和new Vue()中的data不一样
            data(){
                return {
                    uname:''
                }
            },
            created(){
                  console.log(this.$route.params.uname);
                  this.uname = this.$route.params.uname;
            }
        };

        //我们要是用路由来接管我们组件的注册
        var vueRouter = new VueRouter({
          routes:[
              {path:'/',redirect:'login'},
              {name:'login',path:'/login',component:loginComponent},
              {name:'register',path:'/register/:uname',component:registerComponent}
          ]
        })

        //创建vue对象
        new Vue({
            router:vueRouter
        }).$mount('#app')
</script>
```
```
注：params
<body>
      <div id="app">
              <router-link to='/login'>登录</router-link>
              <router-link to='/register'>注册</router-link>

              <router-view></router-view>
      </div>
</body>
<script type="text/javascript">
        //我们这个时候的组件只需要定义不需要注册，路由接管了注册的功能
        //定义登录组件
        var loginComponent = Vue.extend({
            template:'<h2>登录组件的内容</h2>'
        });

        //定义注册组件 --- 定义组件的简写方式
        var registerComponent = {
            template:'<h5>register component content</h5>'
        };

        //我们要是用路由来接管我们组件的注册
        var vueRouter = new VueRouter({
          routes:[
              {path:'/',redirect:'register'},
              {name:'login',path:'/login',component:loginComponent},
              {name:'register',path:'/register',component:registerComponent}
          ]
        })

        //创建vue对象
        new Vue({
            router:vueRouter
        }).$mount('#app')
</script>
```
## vue-resource
```
作用:在Vue中发送网络请求的 GET/POST/JSONP
网址:
	https://github.com/pagekit/vue-resource
	
文档地址:
	https://github.com/pagekit/vue-resource/blob/master/docs/http.md

注意:
	它是一个基于Vue的第三方网络框架
	
	jsonp的Ajax请求需要后台API接口的支持
```
```
注：get
<body>
        <div id="app">
                <button @click='getLogin'>发送GET请求</button>
        </div>
</body>
<script type="text/javascript">
        new Vue({
            el:'#app',
            methods:{
                getLogin(){
                    var url = "http://127.0.0.1:3000/login?username=zhangsan&password=adfafafd";
                    this.$http.get(url).then(res=>{
                        console.log(res.body);
                    },err=>{
                        console.log(err);
                    });
                }
            }
        })
</script>

```
```
注：post
<body>
        <div id="app">
                <button @click='postLogin'>发送POST请求</button>
        </div>
</body>
<script type="text/javascript">
        new Vue({
            el:'#app',
            methods:{
                postLogin(){
                    var url = "http://127.0.0.1:3000/postLogin";
                    //如果是普通的post请求,最后一个就是{emulateJSON:true}
                    this.$http.post(url,{username:'lisi',password:'lisi'},{emulateJSON:true}).then(res=>{
                        console.log(res.body);
                    },err=>{
                        console.log(err);
                    });
                }
            }
        })
</script>
```
```
注：jsonp
<body>
        <div id="app">
                <button @click='getLogin'>发送jsonp请求</button>
        </div>
</body>
<script type="text/javascript">
        new Vue({
            el:'#app',
            methods:{
                getLogin(){
                    var url = "http://127.0.0.1:3000/jsonpLogin?username=laowang&password=xiaowang";
                    this.$http.jsonp(url).then(res=>{
                        console.log(res.body);
                    },err=>{
                        console.log(err);
                    });
                }
            }
        })
</script>
```
## 组件通信
### 抽取评论组件（父传子）
```
为什么要抽取?
	1.评论组件在 新闻详情 图片详情 商品详情中都有
	如果不抽取那么每个模块中都要写,这样代码会很冗余
	2.抽取之后方便以后统一拓展和维护

怎么抽取(抽取的思路)?
	1.将评论组件所有的内容写在一个单独的vue中,比如SubComment.vue中
	2.在需要的组件中(新闻评论、图片详情)进行导入使用即可
	```
		components:{
            subcomment // 导入子组件
        }
	```
	
代码实现:
	具体代码参见项目
	
注意点:
	1.子组件中接收父组件传递过来的参数
		在子组件的export default中写入如下代码
		```
			props:['父组件中绑定的内容的key']
		```
	
	2.mint-ui中给按钮绑定点击事件
		```
			@click = '函数名称'
		```
		
	3.Vue中ref
		http://jingyan.baidu.com/article/acf728fd5ee4acf8e510a3cc.html
		
	4.js中concat函数的使用
		http://www.w3school.com.cn/jsref/jsref_concat_array.asp
```
### 子组件的值传递给父组件this.$emit(子传父)
```
子组件需要做的事:
	1.写好子组件自己的代码
	2.在需要传值给父组件的地方调用
		this.$emit(key,值),注意,这个key等下在父组件中要使用到
		
父组件需要做的事:
	1.导入子组件
	2.在components中注册子组件
	3.在<template></template>中使用子组件
	4.在子组件的标签中,注册接收子组件值的事件
		例如:	
			```
			   <subnumber v-on:key='函数名称'></subnumber>
			```
	5.在父组件的methods中,写好接收子组件传过来的值的函数即可
		例如:
			```
				methods:{
					函数名称(子组件传递过来的值){
						xxxxxx
					}
				}
			```
```
### 非父子组件通信
```
实现步骤:
	1.定义一个公用的vue对象,这个对象专门是用来改变底部Tabbar中购物车
	的徽标(badge)的数字用的
	
	2.在需要传值的组件中(商品信息组件),调用公用vue对象的$emit方法传值
		例如
			```
				vueObj.$emit(key,值)
			```
	3.在需要接收值的组件中(App.vue)中,使用公用的vue对象来注册事件,通过回调函数接收值
		例如
			```
				vueObj.$on(key,function(值){
    				xxx代码
				});
			```
```

## vue-preview插件的使用
```
作用:
	一个Vue集成PhotoSwipe图片预览插件

网址:
	https://www.npmjs.com/package/vue-preview
 	
注意事项:
	1.插件目前仅支持vue2.0以上版本
	2.img标签上的class不能去掉
	3.webpack.config.js 需要配置的地方
```
```
	{
            test: /vue-preview.src.*?js$/,  //表示匹配vue-previe这个组件中的js
            loader: 'babel-loader'  //使用babel-loader解析es6语法
        },
        
        { 
            test: /\.(png|jpg|ttf|svg|gif)$/,
            loader: 'url-loader?limit=4000'
        }
	
	一定要在返回的数据中设置图片的宽度和高度,否则点击看不了全图
```
