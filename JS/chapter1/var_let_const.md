## 1.1 var let const의 차이

ES6 부터 let과 const 가 도입되었고 필요에 맞게 변수를 정의하는 것이 더 용이해졌다!

- var

    var 키워드로 선언된 변수는 함수 스코프에 종속된다.

    for 루프(블록 스코프) 내에서 var 키워드로 변수를 선언하면 이 변수를 for 루프 밖에서도 사용할 수 있다.

    ```jsx
    for (var i= 0; i <10;i++){
    	var leak = "나는 루프밖에서 사용 가능"
    }
    console.log(leak);//나는 var이라 루프밖에서 사용가능

    function myFunc(){
    	var funtionScoped = "나는 함수안에서만 사용가능"
    	console.log(functionScoped);
    }
    myFunc();//나는 함수안에서만 사용가능
    console.log(functionScoped);//not defined;
    ```

    - let

        let(및 const)로 선언된 변수는 블록스코프로 종속되어, 그 변수가 선언된 블록과 그 하위블록 내에서만 사용할 수 있다

        ```jsx
        let x= "global"
        if (x === "global"){
        	let x = "block-scoped"
        	console.log(x); //block-scoped;
        }
        console.log(x); //global, if문 안에서 선언된 x는 If 블록 안에서만 사용됨

        //var을 사용하면
        var y = "global";
        if (y === "global"){
        	var y = "block-scoped";
        	console.log(y)//block-scoped
        }
        console.log(y);//block-scoped, if 문 안에서 y의 값을 바꿔버렸다
        ```

    - const

        let과 마찬가지로 const로 선언된 변수도 블록스코프에 종속되지만, 차이점이라면 재할당을 통해 값이 변경되지 않고 다시 선언되지도 않는다는 것. 

        하지만 const로 선언된 변수가 불변인 것은 아니다.

        객체로 const를 선언하여도, 객체 안의 속성은 변경할 수 있다. 재할당은 불가능

        객체의 내용을 변경할 수 없게 하려면 Object.freeeze(obj); 메서드 활용 가능

        ```jsx
        const constant = "const"
        constant = "바껴라" // 오류

        const obj = {
        	a:1,
        	b:2,
        }  

        obj.a = "a"
        console.log(obj.a); //a, const 안의 속성값 변화

        Object.freeze(obj);
        obj.b= "b";
        console.log(obj.b); // 2, 값이 변하지 않았다
        ```

    ## 1.2 TDZ 일시적 비활성 구역

    예시를 바로 보자

    ```jsx
    console.log(i); //undefined'\
    var i = "나는 var" 

    console.log(j);
    let ; = "나는 let" //j는 초기화되지 않은 값이라고 나옴
    ```

    var let const는 호이스팅의 대상이 된다

    호이스팅현상이란, 변수를 선언, 초기화할때 코드가 실행되기 전에 처리되고 스코프 최상단으로 올라가는것

    var / let, const 차이는

    var은 정의되기 전에도 접근할 수 있다 , 하지만 값에는 접근할 수 없음

    let과 const는 TDZ로 들어가서 접근도 할 수 없다. 

    → 초기화 되기 전에 변수로 접근하여 오류를 발생하는것을 방지한다

    > 결론: var 쓰지 말고 const, let 쓰자!!