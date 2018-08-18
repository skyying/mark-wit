## Design Pattern - Revealing module



如果不想要一再重複的打module.property來新增功能，或者每次要刻意處理public or private的問題。所以乾脆想一個簡單的方法，先讓所有的功能跟變數都是private的，再回傳一個object裏面放所有private的method與object, 寫法跟架構上都更簡潔清楚。



```
var myRevealingModule = (function() {
    var privateVar = "Ben",
        publicVar = "Hey there";

    function privateFunction() {
        console.log("Name" + privateVar);
    }
    function publickSetName(strName) {
        privateVar = strName;
    }
    function publickGetName() {
        privateFunction();
    }
    myRevealingModule.abc = function(){
        console.log("abc");
    }
    return {
        setName: publickSetName,
        greeting: publicVar,
        abc: abc,
        getName: publickGetName,
    };
})();

myRevealingModule.setName("Paul Kinlan");

```

