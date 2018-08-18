# Design Pattern - Modules



數種可以實作modules的方法，



包含 1. the moduel pattern

2. object literal notation
3. AMD modules
4. CommonJS modules
5. ECMAScript Harmony modules



### Object Literals



```
var myObjectLiteral = {
    
    variableKey: variableValue,
    functionKey : function(){
        //...
    }
}
```

可以用這樣來使用

```
myModuel.property = "someValue";
```



```
var myModule = {
    myProperty: "someValue",
    myConfig: {
        useCaching: true,
        language: "en"
    },
    saySomething: function(){
        console.log("somethign you want to say)
    },
    updateConfig: function(newConfig){
        if(typeof newConfig === "object" ){
            this.myConfig = newConfig;
        }
    }
}

myModule.saySomething();
myModuel.updateConfig({
    language: "ch",
    useCaching: false,
})
```



用object literal的好處是可以組織並且封裝你的Code。更多閱讀http://rmurphey.com/blog/2009/10/15/using-objects-to-organize-your-code



### The Module Pattern

簡單的來講就是提供private 和 public 的封裝方法, 在javascript中就是可以提供一種public/private的方法在全域範圍使用。

這裏提供的做法就是使用function scope來保護，在module pattern內，變數和方法都只會在module 內宣告。但取用module return 的變數或方法則是哪裏都可以取用。

這個模式用IIFE，立即被invoke後，會return一個object。



```
var testModule = (
   function(){
       var counter = 0;
       return {
           incrementCounter: function(){
               return counter++;
           },
           resetCounter: function(){
               counter = 0;
           }
       };
       
   })();
   
   // usage:
   
   testModule.incremenetCounter();
   
   testModule.resetCounter();
```



而因爲閉包的關係，只能從外面存取return出來的變數和方法而已，以上面的例子而言，只能從外面存取incrementCounter和resetCounter, 而counter這個變數則是私有3的，只能在module內部被使用。



###  導入Mixins



如何導入其他其他函式庫？可以把函式庫當成變數傳入。

```
var myModule = (function(jQ, _)){
   function priviteMethod1 (){
       jQ(".continaer").html("test");
   }  
   function privateMethod2 (){
       console.log( _.min([10, 5, 100]));
   }
   return {
       publicMethod: function(){
           privateMethod1();
       }
   }
})(jQuery, _);

myModule.publickMethod();
```



### Export 

如何export 在module 內宣告的globel變數呢？

```
var myModule = (function() {
    var module = {},
        privateVarible = "hello world";
    function privateMethod() {
        console.log("privateMethod");
    }
    module.publicProperty = "foobar";
    module.publicMethod = function() {
        console.log(privateVarible);
    };
    return module;
})();

```



這個概念就是在module內再實作另外一個module，最後直接return該module。



![image-20180804102953421](/var/folders/53/jqmxy0dj4bq0f9j399wxt3lr0000gn/T/abnerworks.Typora/image-20180804102953421.png)



如果要用store這個namespace來宣告basket.core這個變數，可以這樣做，可以先檢查store是否存在，如果不存在就宣告一個新的，接着檢查store下backet是否存在，一樣，不存在就宣告新的，依次類推。

```
var store = window.store || {};

if(!store["basket"]){
    store.basket = {};
}

if(!store.basket["core"]){
    store.basket.core = {};
}

store.basket.core = {
    //
}

```





### jQuery

```
//變數是module,如果module.init存在，那就執行它
function library ( module ) {
    $( function(){
        if(module.init){
            module.init();
        }
    });
    return module;
}
// use case, 回傳一個有init method的module
var myLibrary = library (function(){
    return {
        init: function(){
            // module implementation
        }
    };
}());

```



使用module的好處是讓程式碼更有組織，並且把priviate的部分封裝起來。但缺點就是如果有需要將private換成public or public換成private，就得一一處理相關的member。



相關文章 http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html

































