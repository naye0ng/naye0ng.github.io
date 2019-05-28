---
layout: post
title: "모던 자바스크립트 1 - 블록 바인딩"
subtitle: "var, let, const의 차이 및 호이스팅"
author: Nayeong Kim
tags: Javascript
comments : True
---

<div id='preview' class='display-none'>
자바스크립트는 다른 언어와 달리, 변수 선언 방식에 따라 변수의 생성 위치와 스코프가 달라진다. ES6에서는 변수의 스코프를 더 쉽게 제어할 수 있는 옵션을 제공한다. var, let, const 선언의 차이점과 스코프, 호이스팅의 개념에 대해 알아보자.
</div>

##  Javascript : 블록 바인딩

[모던 자바스크립트](http://www.yes24.com/Product/Goods/56029935?Acode=101) 책으로 ECMAScript6를 공부하고 기록한 내용이다.

<br>

자바스크립트는 다른 언어와 달리, 변수 선언 방식에 따라 변수의 생성 위치와 스코프가 달라진다. ES6에서는 변수의 스코프를 더 쉽게 제어할 수 있는 옵션을 제공한다.

<br>

### 1. var 선언과 호이스팅

"왜 기존의 var 선언은 혼란스러울까?"

var 변수를 이용하여 변수를 선언하면 위치와 상관없이 함수의 맨 위(만약 함수의 바깥에서 선언되었다면, 전역스코프)에 있는 것처럼 처리된다. 이를 `호이스팅(Hoisting)`이라 한다.

{% highlight javascript %}
function getValue(condition) {
    if (condition){
        var value = "blue";
        return value;	
    } else {
        // 이 지점에서 value에 접근할 수 있을까? 가능하다.
	return null;
    }
    // 이 지점에서 value에 접근할 수 있을까? 가능하다.
}
{% endhighlight %}

위와 같은 코드를 자바스크립트 엔진은 내부적으로 아래와 같이 변경시킨다.

{% highlight javascript %}
function getValue(condition) {
    var value;
    if (condition){
        value = "blue";
        return value;	
    } else {
        // value = undefined
	return null;
    }
    // value = undefined
}
{% endhighlight %}

value값이 conditon의 값이 True일때 생성될 것이라 생각할테지만 자바스크립트의 호이스팅에 의해 value 변수는 조건문의 참 거짓과 관계없이 생성된다. 뿐만 아니라 함수의 맨 위에서 정의 되므로 else 문 안에서도 접근이 가능하다. 

만약, else문 안에서 value에 접근한다면 함수의 상단에서 선언만 되었지 초기화되지 않았으므로 undefined값을 가진다.

<br>

### 2. 블록-레벨 선언

블록-레벨 선언이란 주어진 블록 스코프 밖에서는 접근이 불가능한 바인딩을 선언하는 것이다. 렉시컬(lexical) 스코프라고도 불리는 블록 스코프는 **함수 내부**, **블록 내부({ })**에 만들어진다.

<br>

#### 2-1. let 선언

let 문법은 기본적으로 var와 비슷하다. 그러나 let으로 선언된 변수의 스코프는 현재의 코드 블록으로 대체된다. **즉, let으로 선언된 변수는 var와 달리 함수의 상단에 호이스팅되지 않는다.** 

{% highlight javascript %}
function getValue(condition) {
    if (condition){
        let value = "blue";
        return value;	
    } else {
        // 이 지점에서 value에 접근할 수 있을까? 불가능하다.
	return null;
    }
    // 이 지점에서 value에 접근할 수 있을까? 불가능하다.
}
{% endhighlight %}

<br>

#### 2-2. 재정의 금지

식별자가 특정 스코트 안에 선언되어 있는 경우, 스코프 안에서 let 선언으로 식별자를 사용하면 당연히 에러가 발생한다.

{% highlight javascript %}
var value = 10;
let value = 40; // error
{% endhighlight %}

반대로, 아래와 같이 let 선언을 이용하여 기존 변수(전역 혹은 블록 외부에 선언된)와 같은 이름으로 새 변수를 블록 스코프 내부에 만드는 것은 가능하다.

{% highlight javascript %}
var value = 10;

if (condition) {
    let value = 40;
}
{% endhighlight %}

이와 같이, let 선언은 블록을 내부에 변수 value를 새로 만드는 것으로 에러를 발생시키지 않는다. 

즉,  블록 외부의 value는 var로 선언된 값 10이 들어가며, if 블록 내부에서는 let으로 선언된 40이 변수 값으로 들어간다.

let은 해당 블록의 실행이 끝날 때까지 전역변수 value에 대한 접근을 막는다. 

<br>

#### 2-3. const 선언

const로 선언된 변수는 상수(constants)로 간주되며, 한번 설정하면 변경할 수 없다. 그러므로 const 변수는 한번 선언할 때 초기화해야 한다.

{% highlight javascript %}
const value1 = 1;

const value2;	// error
{% endhighlight %}

let과 마찬가지로 const도 블록-레벨 선언이다.

이는, 상수 역시 선언된 블록의 바깥에서 접근이 불가능하며, **호이스팅되지 않는다**는 뜻이다. 또한, 같은 블록 내에 같은 이름을 가진 변수는 **재정의할 수 없다.** 
<br>
*(같은 이름의 변수가 var나 let으로 선언된 것은 중요하지 않다.)*

{% highlight javascript %}
var name = "nana"
let age = 26

const name = "haha"	// error
const age = 29 // error
{% endhighlight %}

<br>

#### 2-4. 재할당

let과 const의 차이점은 재할당에 있으며, const 변수의 경우 재할당이 불가능하다. 

{% highlight javascript %}
let name = "nana";
name = "haha";

const age = 26;
age = 29;	// error : 재할당 불가능
{% endhighlight %}

그러나 주의할 점은 상수 객체(const로 선언된 객체)도 수정이 불가능하다고 생각해선 안된다는 점이다.

**const 선언은 바인딩을 변경하지 못하도록 하는 것이지, 바인딩 된 값의 변경을 막는 것이 아니다.** 즉, 객체를 const로 선언해도 객체가 가진값은 수정할 수 있다.

{% highlight javascript %}
const person = {
    name : "nana"
};
// 정상 작동 : 바인딩된 객체는 그대로, 내부의 변수만 바꿈
person.name = "haha";
// error : 바인딩된 객체 전체를 변경하려고 함
person = {
    name : "haha"
}; 
{% endhighlight %}

<br>

#### 2-5. var, let, const 비교

| 선언  |  스코프  | 호이스팅 | 재정의 | 재할당 |
| :---: | :------: | :------: | :----: | :----: |
|  var  | function |    O     |   O    |   O    |
|  let  |  block   |    X     |   X    |   O    |
| const |  block   |    X     |   X    |   X    |

<br>


#### 2-6. TDZ : 임시 접근 불가구역

let이나 const로 선언한 변수는 선언하기 전에 변수에 접근할 수 없다. 코드를 해석할 때 자바스크립트 엔진은 var의 경우 함수 최상단이나 전역 스코프로 호이스팅하지만, let과 const의 경우 TDZ 내에 배치한다. 
<br>
TDZ 내의 변수에 접근하려하면 런타임에러가 발생한다. 변수 선언이 실행된 이후에만 TDZ에서 변수가 제거되며 비로소 변수를 사용할 수 있게된다.

{% highlight javascript %}
// undefined : value가 선언된 블록의 바깥이므로 TDZ와 상관이 없다.
console.log(typeof value); 

if(condition){
    // runtime error : 변수가 TDZ 내에 존재
    console.log(typeof value); 
    let value = "red";
    // String
    console.log(typeof value);
}
{% endhighlight %}

<br>

### 3. 반복문 안에서의 블록 바인딩

블록 레벨 스코프가 기본인 다른 언어에서는 for문 안에서만 i 변수에 접근할 수 있다. 그러나 자바스크립트에서 var 선언이 호이스팅되기 때문에 아래와 같이 for문 바깥에서도 i 변수에 접근할 수 있다.

{% highlight javascript %}
for(var i=0;i<10;i++){
    console.log(i);
}
// 여기서도 여전히 i에 접근 가능하다.
console.log(i);	// 10
{% endhighlight %}

의도대로 for문 안에서만 i 변수에 접근할 수 있도록 하기 위해서는 var대신 let을 사용해야 한다.
<br>
*(const는 재할당이 불가능하므로 for문의 변수로 적합하지 않다.)*

{% highlight javascript %}
for(let i=0;i<10;i++){
    console.log(i);
}
console.log(i);	// error
{% endhighlight %}

<br>

#### 3-1. 반복문 내의 함수

var는 반복문 안에서 사용한 변수를 외부에서도 접근할 수 있도록 하기 때문에 반복문 내부에서 함수를 사용할 때 문제를 야기시켜왔다. 

{% highlight javascript %}
// 호이스팅에 의해 실제 i가 선언되는 위치는 여기!
var funcs = [];

for(var i=0;i<10;i++){
    funcs.push(function(){
        console.log(i);
    })
}

funcs.forEach(function(func){
    func();	// 10이 10번 출력됨 : 전역 스코프 i를 참조한다고 생각하면 된다.
})
{% endhighlight %}

보통은 0부터 10까지 출력될 것으로 생각하지만 숫자 10을 10번 출력한다. i는 반복문 안에서 공유되고 있으므로, 그 안에서 생성된 함수가 모두 같은 변수를 참조하고 있기 때문이다. 그래서 반복문이 완료되면 변수 i는 10이 되므로 console.log(i)는 호출할 때마다 같은 값을 출력한다.

보통은 이 문제를 해결하기 위해 아래와 같이 **즉시 실행 함수 표현식**을 이용하여 반복 생성하는 변수의 새 복사본을 강제로 만든다.

{% highlight javascript %}
var funcs = [];

for(var i=0;i<10;i++){
    funcs.push((function(value){
        return function(){
            console.log(value);
        }
    }(i)));
}

funcs.forEach(function(func){
    func();	// 0 ~ 9까지의 값이 출력된다.
})
{% endhighlight %}

함수를 선언하고 즉시 실행시키는 방식을 사용한다. 즉 ((functoin(){}을 정의하고 바로 (i)를 인자로 내보내어) 함수를 한번 실행하는 것으로 복사본을 생성하여) funcs에 저장하는 방법을 사용한다.

다행히, ES6부터 let과 const의 블록바인딩으로 이 반복문을 간단하게 해결할 수 있게 되었다.

<br>

#### 3-2. 반복문에서의 let 선언

let 선언은 앞의 즉시 실행 함수 표현식의 동작을 동일하게 수행하여 효과적으로 반복문을 간결하게 만든다. 각 반복 시에 반복문은 새 변수를 만들고 그것을 이전 반복문에서와 같은 이름의 변수값으로 초기화 한다. 

{% highlight javascript %}
var funcs = [];

for(let i=0;i<10;i++){
    funcs.push(function(){
        console.log(i);
    })
}

funcs.forEach(function(func){
    func();	// 10이 10번 출력됨 : 전역 스코프 i를 참조한다고 생각하면 된다.
})
{% endhighlight %}

> 반복문 안에서 let 선언의 동작은 명세에 특별하게 정의된 동작이며 호이스팅되지 않는 특성과는 관련이 없다. 이 부분은 표준화 진행 과정 중 추가된 것으로 let의 초기 구현에는 이러한 내용이 없었다.

<br>

#### 3-3. 반복문 안에서의 const 선언

{% highlight javascript %}
var funcs = [];
// error : 반복문이 한 번 수행되도 에러 발생
for(const i=0;i<10;i++){
    funcs.push(function(){
        console.log(i);
    })
}
{% endhighlight %}

변수 초기화에 const를 사용할 수 있지만, 상수 값을 변경하려고 하면 에러가 발생한다. 

반대로 말하면, 변수를 수정하지 않는 경우에는 반복문의 초기화부분에 const를 사용해도 된다.

{% highlight javascript %}
var funcs = [], 
    object = {
        a:true,
        b:true,
        c:true,
    };

for (const key in object){
    funcs.push(function(){
        console.log(key);
    });
}

funcs.forEach(function(func){
    func()	// "a", "b", "c" 출력
})
{% endhighlight %}

이 코드에서 에러가 발생하지 않는 이유는 무엇일까? 반복문의 초기화 부분에서 let과 마찬가지로 기존의 바인딩 되었던 값을 변경하지 않고 매번 새로운 바인딩을 만들기 때문이다.

<br>

### 4. 전역 블록 바인딩

전역 스코프에서 let과 const는 var와는 다르게 동작한다. 만약 var를 전역 스코프에서 사용하면 전역 객체(브라우저의 window객체)의 프로퍼티로 새로운 전역변수를 생성한다. 이는 뜻하지 않게 전역변수를 var로 덮어쓸 수도 있다는 뜻이다.

{% highlight javascript %}
var RegExp = "hello";
console.log(window.RegExp);	// "hello"
{% endhighlight %}

반대로, 전역 스코프에서 var대신 let과 const를 사용하면, 새로운 바인딩이 전역 스코프에 추가되지만 전역 객체의 프로퍼티로 추가되지는 않는다. 

즉, let이나 const로는 전역 변수를 덮어 쓸수 없으며, 일시적으로 전역 스코프의 전역 변수 프로퍼티 대신 사용한다는 의미이다.

{% highlight javascript %}
let RegExp = "hello";
console.log(RegExp);	// "hello"
console.log(window.RegExp === RegExp);	// false
{% endhighlight %}

let으로 선언한  RegExp와 window.RegExp는 일치하지 않으므로전역 스코프에 영향을 주지 않음을 확인할 수 있다.

즉, let과 const에는 전역 객체 수정 기능이 없으므로, 전역 프로퍼티를 생성하고 싶지 않을 때 사용하면 전역 스코프를 안전하게 사용할 수 있다.

<br>

### 5. 블록 바인딩을 위한 모범 사례

const를 기본으로 사용하고 변수 값을 변경해야하는 경우에만 let을 사용하자. 예상하지 못한 값 변경은 버그의 원인이 될 수 있기 때문이다.

<br>

### 6. var, let, const 를 사용하지 않은 경우

변수 키워드를 사용하지 않으면 함수/블록 안에서 선언되더라도 **무조건 전역변수**로 취급된다.

{% highlight javascript %}
function myFunc(){
    for (p=0;p<1;p++){
        console.log(p);	// 0
    }
    console.log(p);	// 1
}
myFunc()
console.log(p);	// 1
{% endhighlight %}

