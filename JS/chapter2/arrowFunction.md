## 2.1 화살표 함수

ES6에서 처음으로 도입된 함수 선언 방법입니다

이전 함수선언에는 함수 정의, 함수 선언 방식이 있다

```jsx
function myFunc(name){
	 return "hello " + name; } //함수 정의하기

const myFunc2 = function(name){
	return "hello " + name;} //함수 선언하기

const myFunc3 = (name) => {
	return ("hello " + name)} //화살표 함수
	// 변수 = (괄호안에 파라미터) => {화살표 이후 "{}" }
```

```jsx
const myFunc = () => { return "Hello" }; //파라미터가 없으면 빈 괄호를, 템플릿 리터럴
const myFunc2 = name => {return "Hello " + name} // 파라미터가 하나면 괄호 생략 가능
```

## 2.2 암시적 반환

명시적 반환 : return 키워드를 사용해서 값을 반환해주는것

암시적 반환 :  return 키워드 생략해서 반환 가능

화살표 함수를 사용하면 명시적 반환을 생략할 수 있다

```jsx
const oldFunction = function(name) {
	return "Hello " + name;
}; //ES5 함수

const arrowFunction = name => `Hello {$name}`
//화살표 함수

//같은 결과지만 코드가 훨씬 간결해진다
```

객체 리터럴을 암시적 반환하려면 다음과 같이 코드를 쓸 수 있다

```jsx
const race = "100m dash"
const runners = ["Usain Bolt" , "Justin Gatlin", "Asafa Powell"];

const result = 
	runners.map((runner , i )=> ({name:runner, race, place:1+i})); //암시적반환

console.log(result);
```

암시적 반환을 위해서 전체를 ()안에 넣어주면 가능하다

## 2.3 화살표 함수는 익명 함수

예제에서 보는것 처럼 화살표 함수는 익명 함수이다

참조할 이름이 필요한 경우 함수를 변수에 할당하면 된다

```jsx
const greeting = name => `hello ${name}` //변수에 함수 할당

greeting("sangjun");
```

## 2.4 화살표 함수와 this 키워드

> 여기가 가장 중요한 파트, 코드가 간결해지는 것 말고도 함수 선언 방법과 화살표 함수의 차이가 여기에 있다

화살표 함수 내부에서 this 키워드를 사용할때는 일반 함수와 다르게 동작하므로 주의하여야 한다.

화살표 함수를 사용할때 this 키워드는 상위 스코프에서 상속된다!?

### 가리키는 this 의 차이

1. 일반 함수 사용시 문제점 

```html
<head>

    <script src="./index.js"></script>
    <link href="./index.css" rel="stylesheet" type="text/css">
</head>

<body>
    <div class="box open">
        this is a box
    </div>

</body>

<!-- css -->
.opening {
  background-color: red;
}

```

```jsx
window.onload = function () {
  const box = document.querySelector(".box");

  box.addEventListener("click", function () {
    console.log(this); // box 태그, <div class="box open opening"> this is a box </div>
    console.log(this.classList);
    this.classList.toggle("opening");
    setTimeout(function () {
      console.log(this); //window 객체
      console.log(this.classList); //undefined
      this.classList.toggle("opening");
    }, 500);
  });
};
```

주목해서 보아야 할 곳은 addEventListener 안의 this와

setTimeOut 안의 this가 가리키는 곳이 다르다는 것이다

함수안에서 선언된 this → 함수를 가리킨다.

기본 메서드에서 사용되는 this→ 기본값이 윈도우객체를 가리킨다

여기서 화살표 함수를 사용하면 가리키는 this 값이 달라진다

2. 화살표함수가 가리키는 this

```jsx
//index.js 파일 수정

window.onload = function () {
  const box = document.querySelector(".box");

  box.addEventListener("click", function () {
    console.log(this); // box 태그, <div class="box open opening"> this is a box </div>
    console.log(this.classList);
    this.classList.toggle("opening");
    setTimeout(() => {
      console.log(this); //box 태그.
      console.log(this.classList); //box태그 안의 classList
      this.classList.toggle("opening");
    }, 500);
  });
};

```

## 2.5 화살표 함수를 피해야 하는 경우

1.  함수 선언 방식과 화살표 함수로 사용할때 가리키는 this가 다르니 주의해야함!!

```jsx
const button = document.querySelector("btn");
button.addEventListenser("click", ()=>{ 
this.classList.toggle("on")});//여기서 this는 Window객체를 가리킴.

/////

const persoon1 = {
	age:10,
	grow: function(){
		this.age++;
		console.log(this.age};
	 },
};

person.grow();

const person2 = {
	age: 10,
	grow: ()=>{
		//여기서 this는 Window 객체를 가리킴
		this.age++;
		console.log(this.age)
	},
};

person2.grow();
 

```


2. arguments 객체에 대한 접근방식이 다름

```jsx
function example(){
	console.log(arguments[0]};

example(1,2,3);
//일반 함수 선언형에서 arguments 사용 방법

```

```jsx
const showWinner = () => {
	const winner = arguments[0];
	console.log(`${winner} was the winner`);
 
};

showWinner("Sangjun", "jungWan" , "Sangmin");
//오류 , showWinner의 상위스코프는 Window, Window에는 arguments가 없다?

const showWinner = (...args) => {  //이런식으로 파라미터 넣어줘야한다..?
		const winner = ...args[0];
	  console.log(`${winner} was the winner`); 
	};
}
showWinner("Sangjun", "jungWan" , "Sangmin");
// Sangjun was the winner.
```

함수 정의방식 에서 사용하는 arguments 를 화살표함수에서 사용하려면 ...arg같은 방법으로 받아와야 한다