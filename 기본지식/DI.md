#### IoC와 연관해서 DI까지..😅

### 의존관계 주입 = DI(Dependency Iniection)
> 의존관계는 "의존대상 B가 변하면, 그것이 A에도 영향이 미친다."로 정의한다. 결국에는 B의 기능이 수정되는 경우가 발생하면 A에 영향이 미친다는 뜻으로 해석이 된다. (토비의 스프링 참고)
<br>

* DI란 외부에서 두 객체 간의 관계를 결정해주는 디자인 패턴이다.
* **인터페이스를 사이에 둬서 클래스 레벨에서는 의존관계가 고정되지 않도록 한다.(핵심)**
* 런타임 시에 관계를 동적으로 주입하여 유연성을 확보하고 결합도를 낮출 수 있게 해준다.
<br>

#### 📌 의존관계 주입이 아닌 예시
* SchoolUse 클래스 내부에서 Schoole 클래스를 직접 생성하여 사용하면 SchoolUse와 Schoole 클래스의 결합력은 높다.
* 즉, SchoolUse에서 생성한 Schoole 클래스의 '홍길동' 이름이 변경된다면 SchoolUse 자체를 변경해줘야한다. 
```
public class School {
    private String schoolName;
    private Number studentCount;

    public School(String schoolName, Number studentCount){
        this.schoolName = schoolName;
        this.studentCount = studentCount;
    }
}

public class SchoolUse {
    private School school;

    public SchoolUse {
        school = new School('홍길동', 33);
    }
}
```
<br>

#### 📌 의존관계 주입 예시
* 외부 EducationDepartment 클래스에서 생성한다면 수정사항이 생겨도 외부 클래스에서만 수정해주면 되기 때문에 기존의 School, SchoolUse 클래스에서는 변경사항이 없다.
* 즉, '홍길동' -> '고길동'으로 변경하고 싶다면 EducationDepartment 클래스에서 School 생성자를 생성한 곳에서 수정해주면 된다.
```
public class School {
    private String schoolName;
    private Number studentCount;

    public School(String schoolName, Number studentCount){
        this.schoolName = schoolName;
        this.studentCount = studentCount;
    }
}

public class SchoolUse {
    private School school;

    public SchoolUse(School, school) {
        this.school = school;       
    }
}

class EducationDepartment {
    School school = new School('홍길동', 33);

    SchoolUse schoolUse = new SchoolUse(school);
}
```
<br>

#### 📌 결론...
* 위의 의존관계 주입 예시의 School, SchoolUse 클래스는 다른 외부 클래스에서 생성할 수 있는 재사용성이 높은 코드가 된다.
* 결합도가 낮아지면서 의존성이 줄어든다.
* 테스트하기 좋은 코드, 가독성이 높은 코드가 된다.
* **결국에는 내가 만들어도 남이 자유롭게 가져가서 사용할 수 있는 코드로 만든다고 생각하면 될 것 같다. :innocent:**
