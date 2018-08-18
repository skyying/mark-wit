

`let`只在該scope內存活，for loop內的counter就很適合用let,

`var`是用來宣告全域變數用的，所以在global的scope內都有效



for迴圈在條件式內是一個作用域，循環體內又是一個作用域。



`let`新增了block scope,

```
function f(){
    let n = 5;
    if(true){
        let n = 10;
    }
    console.log(n); // 5
}
```



內層可以定義外層的同名變量，但外層無法讀取內層的作用域變量。



```
{{{{
    {let insane = "hello world"}
    console.log(insane) // error
}}}}
```



```
{{{{
    let insane = "hello world";
    {let insane = "hello world";}
}}}}
```



塊級作用域讓IIFE不必要了。

因爲在該block內宣告的let variable都只存活在這個scope, 





es5禁止在function內宣告函數。

```
if(true){
    function f(){}
}

try{
    function f(){
        // code here
    } catch(e){
        // code here
    }
}
```

上面兩種在es5都是違法的。









