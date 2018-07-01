
🥁[Demo](https://skyying.github.io/Javascript-30/01%20-%20JavaScript%20Drum%20Kit/index-START.html), [Code](https://github.com/skyying/Javascript-30/tree/master/01%20-%20JavaScript%20Drum%20Kit)

## How to select element

#### document.querySelector

可以用querySelector來選擇指定的元素，querySelector是深度優先，他會選擇第一個符合條件的元素。

```
let element = document.querySelector(".myClass");
```
傳回第一個遇到的`class name` 是 `"myClass"`的元素。找不到的話會`return null`


在`drum kit`的範例中，有這個選法，可以指定`attribute`來`filter`。

```
const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
```
<br>
#### document.querySelectorAll

傳回符合指定條件的所有`Element`

```
const matches = documents.querySelectorAll("div");
```

上面會傳回所有`div`的`element`

```
const matches = documents.querySelectorAll("div.highlighted > p")
```

傳回所有`class name`是`.highlighted`的`div`元素的`子 <p>`元素。

<br>

## 🎧 Audio on web

`html5` 提供`<audio> tag`, 可以放到`html`內。用選擇器宣導這個`audio element`, 再`play`它。

<br>

#### Example on W3C

```
<audio controls>
 <source src="horse.ogg" type="audio/ogg">
 <source src="horse.ogg" type="audio/ogg">
</audio>
```

<br>

#### 🥁 Drum kit 範例的寫法

##### HTML

```html
<audio data-key="65" src="sounds/clap.wav"></audio>
```
其中的`data-key`是爲了讓`Selector`可以找到指定的`Audio`的條件。

##### Javascript

這次用到兩個功能，一個是currentTime, 另一個是play

* **currentTime**,每次要重播之前，可以把`currentTime`設爲0, 才不會按了之後是往下播而不是重播。

```
audio.currentTime = 0;
```

* **play** ，對`audio`執行 `play()`, 開始播放該元素。

```
audio.play()
```

<br/>


## Control animation

### Detect transition end


使用這每次按一個按扭，會觸發一個CSS 動畫，這裏讓我們知道怎麼監聽動畫結束的事件，之後再執行其他`function`

```
keys.forEach(key => key.addEventListener("transitionend", removeTransition));

```

這裏的做法就是，當點擊到特定的key時，會再該`element`上加上指定的動畫`class`, 然後等到該動畫結束，就移除該`class`. 

其他的動畫相關的事件還有	

### CSS Animation Events

* `animationstart`
* `animationend`
* `animationiteration`

### CSS Transition Events

* `transitionstart`
* `transitionend`
* `transitioncancel`
* `trasitionrun`
