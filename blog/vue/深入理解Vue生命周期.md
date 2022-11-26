https://juejin.cn/post/7095372672040697863
Vue 的父组件和子组件生命周期钩子函数执行顺序可以归类为以下 4 部分：

-   ### 加载渲染过程
    
    父beforeCreate -> 父created -> 父beforeMount -> 子beforCreate -> 子created -> 子beforeMount -> 子mounted -> 父mounted
-   ### 子组件更新过程
    

父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父 updated

-   ### 父组件更新过程
    

父 beforeUpdate -> 父 updated

-   ### 销毁过程
    

父 beforeDestroy -> 子 beforeDestroy -> 子 destroyed -> 父 destroyed
