함수에 디폴트 값을 넣는 방법

ES6 이전에는

```jsx
function getLocation(city,country,continent){
  if(typeof country === 'undefined'){ //if문으로 일일이 확인해줬어야했다
    country = 'Italy'
  }
  if(typeof continent === 'undefined'){
    continent = 'Europe'
  }
  console.log(continent,country,city)
}

getLocation('Milan')
// Europe Italy Milan 뒷쪽부터 

getLocation('Paris','France')
// Europe France Paris

```

```jsx

//처음 받는 값부터 기본값을 넣으려면
function getLocation(continent,country,city){
  if(typeof country === 'undefined'){ //if문으로 일일이 확인해줬어야했다
    country = 'Italy'
  }
  if(typeof continent === 'undefined'){
    continent = 'Europe'
  }
  console.log(continent,country,city)
}

getLocation(undefined, undefined, 'Milan')
// Europe Italy Milan 
getLocation(undefined, 'Paris', 'France')
// Europe France Paris

```

## 3.2 함수 기본값 인수

ES6 문법을 활용해서 함수 기본값 인수를 매우 쉽게 설정할 수 있다.

```jsx
function calculatePrice(total, tax = 0.1, tip = 0.05){
// 세금과 팁에 인수가 없으면, tax = 0.1 , tip = 0.05 가 들어간다
return total + (total * tax) + (total * tip);
}

calculatePrice(100, 0.15);
// 100 0.15 0.05하지만 이경우 두번째 인수는 무조건 tax로 들어간다.
calculatePrice(100, undefined,  0.15);
// 100, 0.1 ,0.15이렇게 undefined 값을 할당해줄 수 있다 
```

### 디스트럭쳐링 사용한 함수 기본값 설정

```jsx
function calculatePrice({total = 0, tax = 0.1 , tip = 0.05} = {}){
	return total + (total * tax) + (total * tip);
};

const bill = calculatePrice({tip : 0.15, total : 150});
```

({total = 0, tax = 0.1 , tip = 0.05} = {}) 부분은 디스트럭쳐링. 비구조화 할당 

뒤에 빈 객체 설정을 해주어야 인수를 기본적으로 객체로 설정한다

```jsx
function calculatePrice({
  total = 0,
  tax = 0.1,
  tip = 0.05}){
  return total + (total * tax) + (total * tip);
}
calculatePrice({});
// cannot read property `total` of 'undefined' or 'null'.
calculatePrice();
// cannot read property `total` of 'undefined' or 'null'.
calculatePrice(undefined)
// cannot read property `total` of 'undefined' or 'null'.
```

디스트럭쳐링은 6장에 내용 있다고 하니

```jsx
function calculatePrice({total = 0, tax = 0.1 , tip = 0.05} = {})
```

이 사용방식을 잘 알아두자