### 문자열, 표현식 삽입 함수 전달

> `` 백틱으로 감싸고, ${}를 사용하기

1. 문자열 삽입

    ```jsx
    var name = "Alberto";
    var greeting = 'Hello my name is ' + name;
    console.log(greeting);

    let name  = "Alberto";
    const greeting = `Hello my name is ${name}`; //``백틱과 ${}
    console.log(greeting);
    // Hello my name is Alberto
    ```

2. 표현식 삽입

    ```jsx
    var a = 1;
    var b = 10;
    console.log('1 * 10 is ' + ( a * b)); //괄호 안에 표현식을 넣었었는데
    // 1 * 10 is 10

    var a = 1;
    var b = 10;
    console.log(`1 * 10 is ${a * b}`); //백틱과 ${} 사용해서 표현식 사용가능
    // 1 * 10 is 10
    ```

3. 함수 전달하기

    ```jsx
    const groceries = {
      meat: "pork chop",
      veggie: "salad",
      fruit: "apple",
      others: ['mushrooms', 'instant noodles', 'instant soup'],
    }

    // this function will map each individual value of our groceries
    function groceryList(others) {
      return `
        <p>
          ${others.map( other => ` <span>${other}</span>`).join('\n')}
        </p>
      `;
    }

    const markup = `
      <div>
        <p>${groceries.meat}</p>
        <p>${groceries.veggie}</p>
        <p>${groceries.fruit}</p>
        <p>${groceryList(groceries.others)}</p> 
      <div>
    `
    // 백틱과 ${} 사용하기

    //  <div>
    //     <p>pork chop</p>
    //     <p>salad</p>
    //     <p>apple</p>
    //     <p>
    //     <p>
    //        <span>mushrooms</span>
    //        <span>instant noodles</span>
    //        <span>instant soup</span>
    //     </p>
    //   </p>
    //   <div>
    ```

### 탬플릿 문자열에 로직을 추가하기

삼항 연산자를 사용한다

```jsx
// create an artist with name and age
const artist = {
  name: "Bon Jovi",
  age: 56,
};

// only if the artist object has a song property we then add it to our paragraph, otherwise we return nothing
const text = `
  <div>
    <p>  ${artist.name} is ${artist.age} years old ${artist.song ? `and wrote the song ${artist.song}` : '' }
    </p>
  </div>
`

// <div>
//  <p>  Bon Jovi is 56 years old
//  </p>
// </div>
const artist = {
  name: "Trent Reznor",
  age: 53,
  song: 'Hurt'
};
// <div>
//   <p>  Trent Reznor is 53 years old and wrote the song Hurt
//   </p>
// </div>
```

위의 예시에서는

${아티스트네임}    ~~~  ${아티스트 에이지} ~~~${아티스트 송  ? true:false } 이런 구조

문자, 표현식,함수 등 표현할 문자열을 ${} 안에 담으면 된다

### 중첩 탬플릿

백틱 안에 또 백틱 쓴거임 그래서 중첩

```jsx
const people = [{
	name: 'Alberto',
	age: 27
},{
	name: 'Caroline',
	age: 27
},{
	name: 'Josh',
	age: 31
}];

const markup = `
<ul>
  ${people.map(person => `<li>  ${person.name}</li>`)}
</ul>
`;
console.log(markup);

// <ul>
//   <li>  Alberto</li>,<li>  Caroline</li>,<li>  Josh</li>
// </ul>
```

### 태그된 탬플릿 리터럴

함수를 태그하여 탬플릿 리터럴을 실행하면, 탬플릿 내부의 모든 항목이 태그된 함수의 인수로 제공된다!!!

함수 이름을 가져다 실행할 탬플릿 앞에 쓰면 된다

```jsx
let person = "Alberto";
let age = 25;

function myTag(strings,personName,personAge){
  let str = strings[1];
  let ageStr;

  personAge > 50 ? ageStr = "grandpa" : ageStr = "youngster";

  return personName + str + ageStr;
}

let sentence = myTag`${person} is a ${age}`;
console.log(sentence);
// Alberto is a youngster
```

 특징
- 첫번째 인수에는 전체 문자열 중 탬플릿 리터럴 변수를 제외한 문자열들이 담긴 배열로 설정되고, 템플릿 리터럴 변수들이 나머지 인수가 된다
- 첫번째 인수에 들어가는 문자열은 탬플릿 리터럴 변수 들을 구분자로 나눈것!!