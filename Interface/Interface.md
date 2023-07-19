#### 📌 인터페이스가 궁금해진 이유?
문득.. 인터페이스를 많이 사용하지만 구체적으로 알고 있지 않다고 생각이 들었다.😳<br>
왜 인터페이스를 사용했지?부터 과거 실무에서 썼던 코드들을 회상하게 되었고 이 기회에 조금 더 파악하고 사용하고 싶어졌다.
<br><br>
### ⭐ 인터페이스 알고 쓰자!
* **인터페이스는 상호 간에 정의한 약속 또는 규칙을 의미한다.**
  * 만약 인터페이스 객체에 아래 코드처럼 명시되어 있다면 name은 string으로, age는 number 타입으로 약속했다고 생각하면 된다.
    <br><pre>interface Student{<br>  name: string;<br>  age: number;<br>}</pre><br>
* **함수의 파라미터에 인터페이스를 적용한다면 명시적으로 사용할 수 있다.**
  * 즉, 객체 그대로 프로퍼티를 보여주는 것이 아닌 인터페이스로 분리해서 타입을 정의한다고 생각하면 될 것 같다.
  <br><pre>interface Student{<br>  name: string;<br>  age: number;<br>}<br><br>const studentA: Student = {<br>  name:'홍길동';<br>  age: 20;<br>}</pre><br>
* **인터페이스에 정의되어 있는 속성들을 전부 사용하지 않아도 된다.**
  * ?로 옵션 설정을 해주면 되는데 만약 옵션 설정을 하지 않았다면 인터페이스에 정의된 구조를 그 값으로 가지게 된다.
    <br> 즉, name, skill 있다면 name, skill 전부를 가지고 있어야 하고 skill이 옵션이라면 name만 가지고 있어도 된다.
    <br><pre>interface Developer{<br>  name: string;<br>  skill?: string;<br>}<br><br>function fun(developer: Developer){<br>  return {<br>    name: '홍길동',<br>  };<br>}</pre><br>
* **인터페이스를 readonly 속성으로 만들 수 있다.**
  * 인터페이스를 처음 생성하고 값을 바꾸지 않는다면 readonly 속성을 사용한다. 이후 값을 변경하려고 하면 에러가 난다.
    <br><pre>interface Developer{<br>  readonly name: string;<br>  skill: string;<br>}<br><br> const developer: Developer = {<br>  name:'홍길동',<br>  skill:TypeScript,<br>}<br><br>developer.name='이순신'; // Error!!!</pre><br> 
* **함수 타입을 정의할 수 있다.**
  * (age: number): boolean; <- 이런식으로 객체 안에 파라미터 타입과 리턴 타입을 정의할 수 있다.<br>
    age는 number 타입으로 파라미터가 들어가고 리턴값은 boolean으로 반환된다.<br><br>
* **인터페이스로 설계도를 만들고 클래스에서 구현해서 사용한다.**
  * 클래스의 선언뒤에 implements 뒤에 인터페이스를 사용한다면 인터페이스를 반드시 구현해야한다.
