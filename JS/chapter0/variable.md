## 0.0 자바스크립트 시작

- 자바스크립트의 역사와 그 이름의 기원에 대해 자세히 알고싶다면.

    → https://medium.com/@benastontweet/lesson-1a-the-history-of-javascript-8c1ce3bffb17

- 자바스크립트 삽입 방법

    HTML 페이지에 자바스크립트를 삽입하는 방법은 두가지 방법이 있다.

    1. <script> 태그 안에 코드 직접 삽입하기

        type 속성을 사용해서 작성한다.

        <script type="text/javascript"> [여기에 자바스크립트 코드 작성] </script>

    2. 외부파일 참조하기
        - 프로젝트 루트로부터 절대경로로 참조하기
        - 상대경로로 참조하기
        - URL로 참조하기

        모두 src 속성에 알맞은 주소를 넣어주면 된다.

        예시:
        ```javascript
        <script src="/home/script.js">절대경로 </script>

        <script src="./script.js">상대경로</script>

        <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/core.js">제이쿼리 url 참조하기</script>
        ```
    ## 0.1 변수

    변수란 값을 담기 위한 공간이다. 오늘날에는 변수를 선언하는 세가지 방법이 있다

    > var  const  let

    1장에서 다시 다루기 때문에 0장에서는 가볍게 보고 넘어간다

    ```jsx
    var , let → 재할당 가능

    const → 새 값을 할당할 수 없다.
    ```

    자세한 차이는 스코프에 대해서 알아야 한다고 하는데 다음장에서 설명해주겠지

    !! let과 const의 적절한 사용법에 대해서는 의견이 많지만, 재할당 해야하는 상황이 아니라면 const를 사용하는게 좋다고 한다

    일단 const로 작성하고 나서, 나중에 재할당이 필요할때 디버깅 과정에서 const를 let으로 고쳐주기!

    ### 변수 명명법

    - 변수명은 숫자로 시작 할 수 없다
    - 변수명에는 공백, 기호 마침표가 들어갈 수 없다.
    - 언어 자체에서 예약어로 쓰이는 단어는 사용할 수 없다

        ex) const let var function class return typeoff try false 등등 자바스크립트에서 사용하는 단어

    ## 0.2자료형

    자바스크립트는 동적 언어이므로, 정적 언어와 달리 변수를 정의할 때 자료형을 정의할 필요가 없다.

    var num = 123;

    console.log(typeof num); //number

    var str = "string;

    cosole.log(typeof str); //string

    - 자바스크립트에는 총 7개의 자료형이 있다, 6개는 원시 자료형이고 나머지 하나는 객체이다!!

    ### 원시 자료형

    원시자료형 : 객체가 아닌 자료형으로, 메서드를 가지지 않는다

    - string : 문자열 //텍스트 데이터를 나타내는 자료형,
    - number : 숫자 //숫자 나타내는 자료형, JS에는 정수만을 표현하는 자료형이 없다.
    - boolean : 불리언 //참 거짓 나타냄.
    - null : 널 // 값이없음을 나타냄
    - undefined : 정의되지 않음 //정의되지 않은 값을 타타냄
    - symbol : 심벌 (ES6에서 추가된 자료형) //고유하고 변경할수 없는 값을 나타냄

    ### 객체

    원시 자료형에서는 하나의 값만 담을수 있지만. 객체는 여러 속성의 모음을 저장하는데 사용할 수 있다.

    ```jsx

    //{ 키:밸류 } 형태로 여러 속성의 데이터를 담을 수 있다.
    const car = {
    	wheels : 4,
    	color : "red",
    	drive : function(){
    		console.log("부릉부릉")
    		},
    	}
    console.log(Object.keys(car)[0]); //car객체의 0번째 키 반환, wheels 
    console.log(typeof Object.keys(car)[0]); //car객체의 0번째 키의 자료형반환, string
    car.drive(); //함수를 속성에 담고 실행시킬 수도 있다, 부릉부릉

    ```

    ### 빈 객체 생성하기

    객체 생성에는 속성을 선언할 필요가 없다.

    빈 객체를 만드는데에는 두가지 방법이 있다

    ```jsx
    const car = new Object(); //new 연산자 활용한것-> 뭘까?
    const car = {}; //리터럴
    ```

    - new 연산자?

        [연구할게 생겼다](https://www.notion.so/6793ecf662324a10a53de809aa45e9ae) [0]번 new 연산자

    객체에 속성을 추가하는 방법도 두가지가있다.

    추가와 접근 모두 가능하다.

    ```jsx
    car.color = "red";
    car['wheels'] = 4

    console.log(car.wheels); // 점 표기법 , 4
    console.log(car['color']); //점 표기법, 'red'
    ```

    - 여러단어로 이루어진 속성의 경우 점 표기법을 사용할 수 없다
    - 변수에 저장된 키 값을 받아와서 사용할 경우 점 표기법을 사용할 수 없다.

    ```jsx
    const cars= {
    	ferrari:"california",
    	porsche:"911"
    	bugatti:"veyron"
    }
    const key = "ferrari"
    console.log(cars.key) //undefined. 
    console.log(cars['key'])//undefined 
    console.log(cars[key])//california.
    ```

### 객체의 복사

원시 자료형과 달리, 객체를 복사할때는 **참조 방식이 쓰인다!!**

```jsx
let car = {
	color:"red"
}

let secondCar = car;

car.wheels=4;
console.log(car); // {color:"red", wheels:4}
console.log(secondCar); //{color:"red",wheels:4} 세컨드카 객체의 속성에 추가한게 아니어도, 추가되었다

```

여기서 중요시 봐야 할 점,

```jsx
console.log(car == secondCar); // true
console.log(car === secondCar); // true

const emptyObj1 = {};
const emptyObj2 = {};

console.log(emptyObj1 == emptyObj2); //false

const newCar = {
	color :"red",
	wheels:4 }

console.log(car == newCar); //false

```

새 변수에 할당한 객체와 원래 객체를 비교하면

항등연산자 == 와 완전 항등 연산자 === 모두 true 가 반환됨을 알 수 있다.

하지만 빈 객체끼리 비교할때, 동일한 속성을 가진 객체끼리 비교할때는 false가 반환된다.

→ 동일한 객체를 비교할 때만 true를 반환받을 수 있다!!!!

주소를 참조하는것이 아닌, 객체의 복사본을 만들고 싶다면 **Object.assgin({}, obj)**

```jsx
const car = {color:"red"}
const newCar = Object.assign({},car);
car.wheels = 4;

console.log(car); //{color:"red", wheels:4}//
console.log(newCar); //{color:"red"} ///

```

- Object의 메서드 assign

    [연구할게 생겼다](https://www.notion.so/6793ecf662324a10a53de809aa45e9ae) [1] Object.assign

### 배열

객체는 키:밸류 쌍에 데이터를 저장할때, 배열은 순서대로 값을 저장하는 **객체**이다

키 값이 필요하지 않을때, 그냥 목록만 저장하고 싶을때 사용한다

```jsx
const fruitBasket = ['apple','banana','orange'];

console.log(fruitBasket);
//(3) ["apple", "banana", "orange"]
//{0:"apple",1:"banana",3:"orange"}
//키값이 Number이고(index라고함), 밸류가 인덱스 순서에 맞게 나열된 객체!!!
console.log(typeof fruitBasket);
//"object"
console.log(fruitBasket[0]); //apple
//대괄호표기법으로만 접근 가능.

const test = {};
test[Number(0)] = "apple";
//console.log(test) 하면 _proto_ : array 로 뜨지가 않네.
```

- array 는 어떻게 만든거지? 단지 키가 Number 자료형인것만으로는 안되는 듯

    [연구할게 생겼다](https://www.notion.so/6793ecf662324a10a53de809aa45e9ae) [2]array는 어떻게 만들어졌나 

- 배열에는 다양한 메서드들이 있다 정말 많이 쓰이고 유용한 것들이 많으니 다음시간에 연구해보자

    [연구할게 생겼다](https://www.notion.so/6793ecf662324a10a53de809aa45e9ae) [3]배열의 메서드들

### typeof를 사용해서 자료형 확인하기

typeof를 사용하면 변수가 어떤 자료형을 가지고있는지 확인할 수 있다

스트링은 스트링, 넘버는 넘버, 객체는 객체 배열은 배열이 아니고 객체다!

하지만 console.log(null)을 하게 되면??

```jsx
console.log(typeof null)//"object"
```

이것은 자바스크립트의 첫번째 구현에서 발생한 버그라고 한다..

실제로 object는 아닌데 코드상 오류라고함.

참고 링크 → https://2ality.com/2013/10/typeof-null.html

## 0.3 함수

함수는 계산과 작업을 수행하는 도구이다

가장 기본적인 함수 정의의 예를 살펴보면

```jsx
function greet(parameter) {
//statemnet
console.log("hello" + parameter);
}
greet("sangjun"); //hellosangjun

```

- parameter : 매개변수
- statement : 명령문

여기서 중요한 점은, 원시자료형이 함수에 전달될 때는 참조가 아니라 값의 형태로 전달된다는 점이다

 → 해당 값에 대한 변경 사항이 전역적으로 반영되지 않는다!!

하지만 객체나 배열이 전달될 때는 참조로 전달되어 수정사항이 원래 객체에 반영된다!

```jsx
let myInt = 1;

function increase(value){
	return value+=1;
}

console.log(myInt); //1
console.log(increase(myInt)); //2
console.log(myInt); //1, 변수 myInt의 값은 변하지 않았다'
//구지 바꿀려면 myInt = increase(myInt);

let myCar = {color:"red"};

function changeColor(car){
	car.color = "blue";
}
console.log(myCar); //{color:"red"}
changeColor(myCar); 
console.log(myCar); //{color:"blue"} 
```

참조로 전달할때, 값으로 전달할때의 차이를 알아두자

함수를 선언하는 또다른 방법

- 함수 표현식 : const에 함수를 할당하는것
- 익명함수 : 함수 표현식을 통해 함수명을 쓰지 않고 함수를 만드는것
- 화살표함수 : 화살표 사용해서 함수를 선언하는것

```jsx
const greeter = function greet(name){
	console.log("hello " + name)};

const greeter2 = function(name){
	console.log("hello " + name)};

const greeter3 = (name) =>{
	console.log("hello" + name)};

//셋 다 같은 함수.

```

## 0.4 함수 스코프와 this 키워드의 이해

### 스코프

**스코프**란 변수에 접근할 수 있는 위치를 제어한다

- 전역 스코프 : 코드의 어느곳에서나 접근 가능
- 블록스코프 : 변수가 선언된 블록 내부에서만 접근 가능

    여기서 블록은 함수, 루프 등 **중괄호로 구분되는 모든 영역을 의미한다!**

```jsx
var myInt = 1;

if(myInt  === 1){
	var secondInt = 2;
	console.log(secondInt);
}
console.log(secondInt); //2, 블록지정이 안되어있어서 if문의 변수에도 접근

if (secondInt === 2){
	let thirdInt = 3;
	console.log(thirdInt);
}
console.log(thirdInt); //오류, let은 {블록} 안에서만 사용가능
```

let 과 const 는 블록스코프를 가진다!

## this 키워드

this 는 기본적으로 window,

다시 한 번, 정리하자면, this는 기본적으로 window이지만, 객체 메서드, bind call apply, new일 때 this가 바뀝니다. 그리고 이벤트리스너나 기타 라이브러리처럼 this를 내부적으로 바꿀 수도 있으니 항상 this를 확인해보셔야 하고요. 여러분이 선언한 function의 this는 항상 window라는 것 알아두세요. (strict 모드에서는 undefined !!)

????이건 다시 봐야할거 같다

[연구할게 생겼다](https://www.notion.so/6793ecf662324a10a53de809aa45e9ae)[4]this는 무엇인가