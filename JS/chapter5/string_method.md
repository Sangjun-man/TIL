### 5.1 기본적인 문자열 메서드

- indexOf();

    지정된 값이 처음 나타는 위치를 반환한다

    ```jsx
    const str = "this is a short sentence";
    str.indexOf("short")//10

    let short = "short"
    str.indexOf(short)//10
    ```

- slice();

    문자열의 지정된 부분을 새 문자열로 반환한다

    ```jsx
    const str = "this is a short sentence";
    str.slice(4);//" is a short sentence"; , 파라미터로 number 1개를 받으면 -> 그 숫자 
    str.slice(5,7);//"is" , 파라미터로 (n,m)을 받으면 -> n번째부터 m-1번째까지
    ```

- toUpperCase(); / toLowerCase();

    문자열을 모두 대문자 / 소문자로 변환한다

    ```jsx
    const str = "This Is A Short Sentence";
    str.toUpperCase(); // "THIS IS A SHORT SENTENCE"
    str.toLowerCase(); // "this is a short sentence"
    ```

### 5.2 새로운 문자열 메서드

- starsWith();

    매개변수로 받은 값으로 문자열이 시작하는지 확인한다

    ```jsx
    const code = "ABCDEFG";

    code.startsWith("ABB"); //false
    code.startsWith("abc"); //false , startsWith는 대소문자를 구분한다
    code.startsWith("ABC"); //true

    code.startsWith("DEF", 3);// 두번째로 받은 인자 다음부터 검사 시작한다.
    ```

- endsWith();

    매개변수로 전달한 값으로 끝나는지 확인.

    ```jsx
    const code = "ABCDEF";

    code.endsWith("DDD"); //false
    code.endsWith("def"); //false, endsWith는 대소문자 구분한다
    code.endsWith("DEF"); //true

    code.endsWith("CD", 4) // true, 두번째로 받은 인자 숫자만큼 검사한다
    ```

- includes();

    전달한 값이 문자열에 포함되어 있는지 확인한다

    ```jsx
    const code = "ABCDEF";

    code.includes("ABB");
    //false
    code.includes("abc");
    //false , includes는 대소문자 구별
    code.includes("CDE");
    //true
    ```

- repeat();

    받은 인수만큼 문자열을 반복해서 리턴한다

    ```jsx
    let hello = "hi"
    console.log(hello.repeat(4);)
    	//"hihihihi"
    ```