### vue-组件间的通信

#### **1.父子组件的通信**

* **1.父组件利用props向子组件传输数据**

  ​		当props中接收的是父组件传递的引用类型（对象或者是数组）时，在子组件中对数据改变时，父组件中的数据也会相应的改变，因为两者是指向的同一地址内存。如果不想子组件的改变影响父组件可以利用深拷贝，将接受的数据进行深拷贝后在子组件中使用，而不直接操作接受的数据。

* **2.子组件向父组件传递参数利用事件机制**
  子组件通过`this.$emit()`派发事件，父组件利用`v-on`对事件进行监听，实现参数的传递

  ```js
  //子组件：
     this.$emit('changeCart',event.target)/*向父组件派发事件，同时传递参数event.target,后面的参数的个数不限*/
  //父组件：
  <v-cartcontrol :food="food" v-on:changeCart="changeCart"></v-cartcontrol>
  <v-cartcontrol :food="food" @changeCart="changeCart"></v-cartcontrol>
  ```

* **3.利用ref属性可以获取到dom元素或者是子组件，从而可以调用子组件的方法（注意2.0版本用ref取代了el）**
  1、当ref直接定义在dom元素上时，则通过`this.$refs.name`可以获取到dom对dom进行原生的操作.(ref属性不崩使用驼峰命名，获取元素也是)

#### **2.非父子组件的通信**

   * **使用eventBus**

     ```js
     //非父子关系的两个组件之间也需要通信。在简单的场景下，可以使用一个空的 Vue 实例作为事件总线：
     var bus = new Vue()  
     // 触发组件 A 中的事件  
     bus.$emit('id-selected', 1)  
     // 在组件 B 创建的钩子中监听事件  
     bus.$on('id-selected', function (id) {  
       // ...  
     }) 
     ```

     