1.编程式路由跳转到当前路由（参数不变），多次执行会抛出NavigationDuplicated的警告错误？
--路由跳转有两种形式：声明式、编程式
--声明式导航没有这类问题，因为vuerouter底层已经处理好了
声明式导航：router-link
编程式导航：router.push|replace
1.1为什么编程式导航进行路由跳转的时候，就有这种警告错苏呢？
“vue-router”：“3.5.3”：最新的vue-router引入promise
1.2通过给push方式传递相应的成功、失败的回调函数，可以捕获到当前错误，可以解决。

1.3通过底部的代码，可以实现解决错误
this.$router,push({name:"search",params:{keyword:this.keyword},query:{k:this.keyword.toUpperCase()}},()=>{},()=>{})
这种写法：治标不治本，将来在别的组件当中push|replace，编程式导航还是有类似错误。

1.4
this：当前组件实例（search）
this.$router属性：当前的这个属性，属性值VueRouter类的一个实例，当在入口文件注册路由的时候，给组件实例添加$router|$route属性
push：VueRouter属性

function VueRouter(){
    
}
<!-- 原型对象的方法 -->
VueRouter.propotype.push = funtion(){
    <!-- 函数的上下文为VueRouter类的一个实例 -->
}

let $router = new VueRouter();

$router.push(xxx);

this.$router.push();

2.Home模块组件拆分
--先把静态页面完成
--拆分出静态组件
--获取服务器的数据进行展示
--动态业务

3.三级联动组件完成
---由于三级联动，在Home、Search、Detail，把三级联动注册为全局组件。
好处：只需要注册一次，就可以在项目任意地方使用