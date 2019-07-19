### JS的冻结、密封和扩展

- 扩展特性
  - `Object.isExtensible` 方法
  - `Object.preventExtensions` 方法
- 密封特性
  - `Object.isSealed` 方法
  - `Object.seal` 方法
- 冻结特性
  - `Object.isFrozen` 方法
  - `Object.freeze` 方法
    - `浅冻结` 与 `深冻结`



## **扩展特性**

如果一个对象可以添加新的属性，则这个对象是可扩展的。
让这个对象变的不可扩展，也就是不能再有新的属性

我们都知道，我们可以通过`属性描述符`创建属性不可配置对象 [如何让对象属性不可配置或枚举](http://segmentfault.com/a/1190000003882976),
在这里我们可以创建不可扩展属性的对象

### **Object.isExtensible 方法**

MDN：

```
概述
    Object.isExtensible() 方法判断一个对象是否是可扩展的（是否可以在它上面添加新的属性）。
语法
    Object.isExtensible(obj)
参数
    obj 需要检测的对象
```

使用：

```
//新对象默认是可扩展的无论何种方式创建的对象，这里使用的是字面量方式
var empty = {a:1};
console.log(Object.isExtensible(empty) === true);//true

//等价于 使用属性描述符
empty = Object.create({},{
    "a":{
        value : 1,
        configurable : true,//可配置
        enumerable : true,//可枚举
        writable : true//可写
    }
});
console.log(Object.isExtensible(empty) === true);//true

//对象是否可以扩展与对象的属性是否可以配置无关
empty = Object.create({},{
    "a":{
        value : 1,
        configurable : false,//不可配置
        enumerable : true,//可枚举
        writable : true//可写
    }
});
console.log(Object.isExtensible(empty) === true);//true
```

那么我们如何让一个对象变成不可扩展：

### **Object.preventExtensions 方法**

MDN:

```
概述
    Object.preventExtensions() 方法让一个对象变的不可扩展，也就是永远不能再添加新的属性。
语法
    Object.preventExtensions(obj)
参数
    obj 将要变得不可扩展的对象
描述
    如果一个对象可以添加新的属性，则这个对象是可扩展的。
    preventExtensions 可以让这个对象变的不可扩展，也就是不能再有新的属性。
    需要注意的是不可扩展的对象的属性通常仍然可以被删除。
    尝试给一个不可扩展对象添加新属性的操作将会失败，不过可能是静默失败，也可能会抛出 TypeError 异常（严格模式）。        
    Object.preventExtensions 只能阻止一个对象不能再添加新的自身属性，仍然可以为该对象的原型添加属性。
```

使用：

```
(function () {
    //Object.preventExtensions 将原对象变得不可扩展,并且返回原对象.
    var obj = {};
    var obj2 = Object.preventExtensions(obj);
    console.log(obj === obj2);//true

    //新创建的对象默认是可扩展的
    var empty = {};
    console.log(Object.isExtensible(empty) === true);//true
    empty.a = 1;//添加成功

    //将其变为不可扩展对象
    Object.preventExtensions(empty);
    console.log(Object.isExtensible(empty) === false);//true

    //使用传统方式为不可扩展对象添加属性
    empty.b = 2;//静默失败,不抛出错误
    empty["c"] = 3;//静默失败,不抛出错误

    //在严格模式中,为不可扩展对象添加属性将抛出错误
    (function fail(){
        "use strict";
        empty.d = "4";//throws a TypeError
    })();

    //使用 Object.defineProperty方法为不可扩展对象添加新属性会抛出异常
    Object.defineProperty(empty,"e",{value : 5});//抛出 TypeError 异常

    Object.defineProperty(empty,"a",{value : 2});
    console.log(empty.a);//输出2

})();
```

在上述代码的最后两行可以看到如果为当前不可扩展对象 empty 修改属性是成功的，这是因为一个对象的属性是否可以被修改与该对象是否可以扩展无关，而是与该对象在创建的时候是否声明为不可重写有关（[Writable](http://segmentfault.com/a/1190000003882976)）

如果我们想让一个对象的所有属性都`不可配置`同时也不允许为该对象进行`扩展`怎么做：

```
(function () {
    //创建一个对象,同时声明其所有属性均为不可配置且不可写
    var obj = {a :1,b:2,c:3};
    Object.defineProperties(obj,{
       "a":{configurable:false},
       "b":{configurable:false},
       "c":{configurable:false}
    });

    //等价于
    var obj = Object.create({},{
        "a":{value :1,congigurable :false,enumerable :true,writable:true},
        "b":{value :2,congigurable :false,enumerable :true,writable:true},
        "c":{value :3,congigurable :false,enumerable :true,writable:true}
    });

    //将其转化为不可扩展对象
    Object.preventExtensions(obj);

    //测试该对象是否即不可扩展同时其所有属性均不可配置
    console.log(Object.isExtensible(obj) === true);//false
    for(var name of Object.keys(obj)){//遍历该对象的所有可枚举属性名,不包括继承而来的属性
        Object.defineProperty(obj,name,{enumerable:false});//将该属性的 enumerable 特性重新配置为 true
    }//抛出异常
})();
```

虽然说上面的程序实现了需求，但未免太麻烦，这里我们可以使用 JS 对象的另一特性 `密封`

## **密封特性**

密封对象是指那些不可 扩展 的，且所有自身属性都不可配置的（non-configurable）对象。

或则说 密封对象是指那些不能添加新的属性，不能删除已有属性，以及不能修改已有属性的可枚举性、可配置性、可写性，但可能可以修改已有属性的值的对象。

### **Object.isSealed 方法**

MDN：

```
概述 
    Object.isSealed() 方法判断一个对象是否是密封的（sealed）。
语法 
    Object.isSealed(obj)
参数
    obj 将要检测的对象
描述
    如果这个对象是密封的，则返回 true，否则返回 false。
```

使用：

```
(function () {
    //新建的对象默认不是密封的
    var empty = {};
    console.log(Object.isSealed(empty) === false);//true

    //如果把一个空对象变得不可扩展,则它同时也会变成个密封对象.
    Object.preventExtensions(empty);
    console.log(Object.isSealed(empty) === true);//true

    //但如果这个对象不是空对象,则它不会变成密封对象,因为密封对象的所有自身属性必须是不可配置的.
    var hasProp = {fee : "fie foe fum"};
    Object.preventExtensions(hasProp);
    console.log(Object.isSealed(hasProp) === false);//true

    //如果把这个属性变得不可配置,则这个对象也就成了密封对象.
    Object.defineProperty(hasProp,"fee",{configurable : false});
    console.log(Object.isSealed(hasProp) === true);//true
})();
```

### **Object.seal 方法**

MDN：

```
概述
    Object.seal() 方法可以让一个对象密封，并返回被密封后的对象。
    密封对象是指那些不能添加新的属性，不能删除已有属性，以及不能修改已有属性的可枚举性、可配置性、可写性，但可能可以修改已有属性的值的对象。
语法
    Object.seal(obj)
参数
    obj 将要被密封的对象
描述
    通常情况下，一个对象是可扩展的（可以添加新的属性）。
    密封一个对象会让这个对象变的不能添加新属性，且所有已有属性会变的不可配置。
    属性不可配置的效果就是属性变的不可删除，以及一个数据属性不能被重新定义成为访问器属性，或者反之。
    但属性的值仍然可以修改。
    尝试删除一个密封对象的属性或者将某个密封对象的属性从数据属性转换成访问器属性，结果会静默失败或抛出TypeError 异常（严格模式）。
    不会影响从原型链上继承的属性。但 __proto__ (  ) 属性的值也会不能修改。
```

使用：

```
(function () {
    var obj = {             //声明一个对象
        prop:function(){},
        foo:"bar"
    };
    //可以添加新的属性,已有属性的值可以修改,可以删除
    obj.foo = "baz";
    obj.lumpy = "woof";
    delete obj.prop;

    var o = Object.seal(obj);//将 obj 密封,且返回原对象
    console.log(o === obj);//true
    console.log(Object.isSealed(obj) === true);//true

    //仍然可以修改密封对象上的属性的值
    obj.foo = "quux";//修改成功

    //但不能把密封对象的属性进行重新配置,譬如讲数据属性重定义成访问器属性.
    //Object.defineProperty(obj,"foo",{get : function(){return "g";}});//抛出 TypeError

    //任何除修改属性值以外的操作都会失败
    obj.quaxxor = "the friendly duck";//静默失败,属性没有成功添加
    delete obj.foo;//静默失败,属性没有删除成功

    //在严格模式中,会抛出 TypeError 异常
    (function fail(){
        "use strict";
        //delete obj.foo;//抛出 TypeError 异常
        //obj.sparky = "arf";//抛出 TYpeError 异常
    })();

    Object.defineProperty(obj,"ohai",{value :17});//添加属性失败
    Object.defineProperty(obj,"foo",{value : "eit"});//修改成功
    console.log(obj.foo);//“eit”
})();
```

如上面程序所示，将一个对象`密封`后仅能保证该对象`不被扩展`且属性`不可重配置`，但是原属性值却是有可能被修改的，若要达到即`密封`又`不可修改原属性值`可以这样：

```
//创建不可修改值的密封对象
(function () {
    //方式一
    var o = {a:1};
    Object.defineProperty(o,"a",{configurable:false,writable:false});
    Object.preventExtensions(o);
    o.a = 2;
    console.log(o.a);//1
    console.log(Object.isExtensible(o) ===false);//true
    console.log(Object.isSealed(o) === true);//true

    //方式二
    o = Object.create(Object.prototype,{"a":{value :1,writable:false}});
    Object.seal(o);
    o.a = 2;
    console.log(o.a);//1
    console.log(Object.isExtensible(o) ===false);//true
    console.log(Object.isSealed(o) === true);//true
    
    //方式...
})();
```

同样的，虽然实现了需求，依旧可以使用另一特性 `冻结`

## **冻结特性**

一个对象是冻结的（frozen）是指它不可扩展，所有属性都是不可配置的（non-configurable），且所有数据属性（data properties）都是不可写的（non-writable）。

数据属性是值那些没有取值器（getter）或赋值器（setter）的属性。

或则说 冻结对象是指那些不能添加新的属性，不能修改已有属性的值，不能删除已有属性，以及不能修改已有属性的可枚举性、可配置性、可写性的对象。也就是说，这个对象永远是不可变的。

### **Object.isFrozen 方法**

MDN：

```
概述
    Object.isFrozen() 方法判断一个对象是否被冻结（frozen）。
语法
    Object.isFrozen(obj)
参数
obj 被检测的对象
描述
    一个对象是冻结的（frozen）是指它不可扩展，所有属性都是不可配置的（non-configurable），且所有数据属性（data properties）都是不可写的（non-writable）。数据属性是值那些没有取值器（getter）或赋值器（setter）的属性。
```

使用：

```
(function () {
    //一个对象默认是可扩展的,所以他也是非冻结的.
    console.log(Object.isFrozen({}) === false);//true

    //一个不可扩展的空对象同时也是一个冻结对象.一个不可扩展的空对象也是密封对象
    var vacuouslyFrozen = Object.preventExtensions({});
    console.log(Object.isFrozen(vacuouslyFrozen) === true);//true
    console.log(Object.isSealed(vacuouslyFrozen) === true);//true

    //一个非空对象默认也是非冻结的.
    var oneProp = { p:42 };
    console.log(Object.isFrozen(oneProp) === false);//true

    //让这个对象变的不可扩展,并不意味着这个对象变成了冻结对象,因为 p 属性仍然是可以配置的(而且可写的).
    Object.preventExtensions( oneProp );
    console.log(Object.isFrozen(oneProp) === false);//true

    //如果删除了这个属性,则它成为空对象,会成为一个冻结对象.
    delete oneProp.p;
    console.log(Object.isFrozen(oneProp) === true);

    //一个不可扩展的对象,拥有一个不可写但可配置的属性,则它仍然是非冻结的.
    var nonWritable = { e : "plep" };
    Object.preventExtensions(nonWritable);
    Object.defineProperty(nonWritable,"e",{writable : false});//不可写
    console.log(Object.isFrozen(nonWritable) === false);//true

    //把这个属性改为不可配置,会让这个对象成为冻结对象
    Object.defineProperty(nonWritable,"e",{configurable : false});//不可配置
    console.log(Object.isFrozen(nonWritable) === true);//true

    //一个不可扩展的对象,拥有一个不可配置但可写的属性,则它仍然是非冻结的.
    var nonConfigurable = { release : "the kraken!" };
    Object.preventExtensions(nonConfigurable);
    Object.defineProperty(nonConfigurable,"release",{configurable : false});
    console.log(Object.isFrozen(nonConfigurable) === false);//true

    //把这个属性改为不可写,会让这个对象成为冻结对象.
    Object.defineProperty(nonConfigurable,"release",{writable : false});
    console.log(Object.isFrozen(nonConfigurable) === true);//true

    //一个不可扩展的对象,值拥有一个访问器,则它仍然是非冻结的.
    var accessor = {get food(){return "yum";}};//这里使用的是字面值法创建对象,默认可配置
    Object.preventExtensions(accessor);
    console.log(Object.isFrozen(accessor) === false);//true

    //把这个属性改为不可配置,会让这个对象成为冻结对象.
    Object.defineProperty(accessor,"food",{configurable:false});
    console.log(Object.isFrozen(accessor) === true);//true


    //使用 Object.freeze 是冻结一个对象的最方便的方法.
    var frozen = {1:81};
    console.log(Object.isFrozen(frozen) === false);//true
    Object.freeze(frozen);
    console.log(Object.isFrozen(frozen) === true);//true

    //一个冻结对象也是一个密封对象
    console.log(Object.isSealed(frozen) === true);//true

    //一个冻结对象也是一个不可扩展对象
    console.log(Object.isExtensible(frozen) === false);//true

})();
```

### **Object.freeze 方法**

MDN：

```
概述
    Object.freeze() 方法可以冻结一个对象。
    冻结对象是指那些不能添加新的属性，不能修改已有属性的值，不能删除已有属性，以及不能修改已有属性的可枚举性、可配置性、可写性的对象。
    也就是说，这个对象永远是不可变的。该方法返回被冻结的对象。
语法
    Object.freeze(obj)
参数
    obj 将要被冻结的对象
描述
    冻结对象的所有自身属性都不可能以任何方式被修改。
    任何尝试修改该对象的操作都会失败，可能是静默失败，也可能会抛出异常（严格模式中）。
    数据属性的值不可更改，访问器属性（有getter和setter）也同样（但由于是函数调用，给人的错觉是还是可以修改这个属性）。
    如果一个属性的值是个对象，则这个对象中的属性是可以修改的，除非它也是个冻结对象。
```

使用：

```
(function () {
    var obj = {
        prop:function(){},
        foo:"bar"
    };

    //可以添加新的属性,已有的属性可以被修改或删除
    obj.foo = "baz";
    obj.lumpy = "woof";
    delete obj.prop;

    Object.freeze(obj);//冻结

    console.log(Object.isFrozen(obj) === true);//true

    //对冻结对象的任何操作都会失败
    obj.foo = "quux";//静默失败;
    obj.quaxxor = "the friendly duck";//静默失败

    //在严格模式中会抛出 TypeError 异常
    (function () {
        "use strict";
        obj.foo = "sparky";//抛出 TypeError 异常
        delete obj.quaxxor;//抛出 TypeError 异常
        obj.sparky = "arf";//抛出 TypeError 异常
    })();

    //使用 Object.defineProperty方法同样会抛出 TypeError 异常
    Object.defineProperty(obj,"ohai",{value:17});//抛出 TypeError 异常
    Object.defineProperty(obj,"foo",{value:"eit"});//抛出 TypeError 异常
})();
```

如该方法 MDN 的描述所述，倘若一个对象的属性是一个对象，那么对这个外部对象进行冻结，内部对象的属性是依旧可以改变的，这就叫浅冻结，若把外部对象冻结的同时把其所有内部对象甚至是内部的内部无限延伸的对象属性也冻结了，这就叫深冻结。

**浅冻结与深冻结**

```
(function () {
    obj = {
        internal :{}
    };
    Object.freeze(obj);//浅冻结
    obj.internal.a = "aValue";
    console.log(obj.internal.a);//"aValue"

    //想让一个对象变得完全冻结,冻结所有对象中的对象,可以使用下面的函数.
    function deepFreeze(o){
        var prop,propKey;
        Object.freeze(o);//首先冻结第一层对象
        for(propKey in o){
            prop = o[propKey];
            if(!o.hasOwnProperty(propKey) || !(typeof prop === "object") || Object.isFrozen(prop)){
                continue;
            }
            deepFreeze(prop);//递归
        }
    }

    deepFreeze(obj);
    obj.internal.b = "bValue";//静默失败
    console.log(obj.internal.b);//undefined
})();
```



# [JavaScript中的可枚举属性与不可枚举属性](https://www.cnblogs.com/jcz1206/p/9553115.html)



https://www.cnblogs.com/kongxy/p/4618173.html

​    在JavaScript中，对象的属性分为可枚举和不可枚举之分，它们是由属性的enumerable值决定的。可枚举性决定了这个属性能否被for…in查找遍历到。

一、怎么判断属性是否可枚举

  js中基本包装类型的原型属性是不可枚举的，如Object, Array, Number等，如果你写出这样的代码遍历其中的属性：

```
`var` `num = ``new` `Number();``for``(``var` `pro ``in` `num) {``    ``console.log(``"num."` `+ pro + ``" = "` `+ num[pro]);``}`
```

它的输出结果会是空。这是因为Number中内置的属性是不可枚举的，所以不能被for…in访问到。

Object对象的propertyIsEnumerable()方法可以判断此对象是否包含某个属性，并且这个属性是否可枚举。

需要注意的是：如果判断的属性存在于Object对象的原型内，不管它是否可枚举都会返回false。

二、枚举性的作用

属性的枚举性会影响以下三个函数的结果：

for…in

Object.keys()

JSON.stringify

先看一个例子，按如下方法创建kxy对象：

```
`function` `Person() {``    ``this``.name = ``"KXY"``;``}``Person.prototype = {``    ``constructor: Person,``    ``job: ``"student"``,``};` `var` `kxy = ``new` `Person();``Object.defineProperty(kxy, ``"sex"``, {``    ``value: ``"female"``,``    ``enumerable: ``false``});`
```

其中用defineProperty为对象定义了一个名为”sex”的不可枚举属性

接下来做以下验证：

1.

```
`for``(``var` `pro ``in` `kxy) {``    ``console.log(``"kxy."` `+ pro + ``" = "` `+ kxy[pro]);``  ``}`
```

遍历结果：

kxy.name = KXY

*kxy.constructor = function Person() {this.name = "KXY";}kxy.job = student*

 

可以看到除了”sex“之外的属性都遍历到了

[ 个人补充

　　for(var pro in kxy) {
　　　　if(kxy.hasOwnProperty(pro)) console.log("kxy." + pro + " = " + kxy[pro]);
　　}
　　打印结果是：

　　kxy.name = KXY

]

2.

```
`console.log(Object.keys(kxy));`
```

结果：

[![枚举性检验2](https://images0.cnblogs.com/blog/622045/201507/031140081819009.png)](http://images0.cnblogs.com/blog/622045/201507/031140074543396.png)

只包含”name”属性，说明该方法只能返回对象本身具有的可枚举属性。

3.

```
`console.log(JSON.stringify(kxy));`
```

<结果：

[![可枚举性检验3](https://images0.cnblogs.com/blog/622045/201507/031140095854780.png)](http://images0.cnblogs.com/blog/622045/201507/031140091753838.png)

此方法也只能读取对象本身的可枚举属性，并序列化为JSON对象。