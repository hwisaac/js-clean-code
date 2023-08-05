> '내부자 거래' 악취란 객체 지향 설계의 원칙에 어긋나는 코드 설계 방식 중 하나를 말합니다. 이는 **한 객체가 다른 객체의 세부사항이나 내부 상태에 너무 자세하게 알고 있거나 의존하고 있을 때 발생**합니다. 이는 객체 간의 캡슐화를 깨트리며, 강한 결합도(coupling)를 유발합니다. 이로 인해 코드는 유연성과 확장성이 떨어지며, 유지보수가 어려워질 수 있습니다.

그렇다면, 이러한 '내부자 거래' 악취를 개선하는 방법에는 어떤 것들이 있을까요? 첫 번째로 '함수/메서드 옮기기'입니다. 이는 해당 함수가 다루는 정보를 보유하고 있는 객체로 해당 함수를 이동시키는 방식입니다. 이렇게 하면 캡슐화를 유지하고 결합도를 낮출 수 있습니다.

두 번째로는 '모듈로 분리하기'입니다. 같은 기능을 하는 메서드나 필드가 여러 곳에서 사용된다면, 이들을 별도의 모듈로 분리하여 중복을 최소화하고, 해당 기능을 이용하는 객체들 사이의 결합도를 낮출 수 있습니다.

마지막으로는 '위임 숨기기'입니다. 이는 객체가 다른 객체를 통해 일을 처리하게 하되, 그 과정을 외부에서는 알 수 없도록 하는 방법입니다. 이를 통해 객체 간의 의존성을 낮추고, 캡슐화를 강화할 수 있습니다.

다음과 같은 상황을 생각해볼 수 있습니다. 

```javascript
class Employee {
    private String name;
    private Department department;

    public String getDepartmentName() {
        return department.getName();
    }
}

class Department {
    private String name;

    public String getName() {
        return name;
    }
}
```
위의 예에서 `Employee` 클래스는 `Department`의 내부 상태에 접근하고 있습니다. 이 경우 '메서드 옮기기'를 이용하여 `Employee`가 `Department`의 내부 상태에 직접 접근하지 않도록 개선할 수 있습니다.

```javascript
class Employee {
    private String name;
    private Department department;

    public String getDepartmentName() {
        return department.getDepartmentName();
    }
}

class Department {
    private String name;

    public String getDepartmentName() {
        return name;
    }
}
```
이렇게 수정하면, `Department`의 내부 상태는 `Department` 내부에서만 관리되며, `Employee`는 `Department`의 메서드만을 통해 필요한 정보를 얻게 됩니다. 이렇게 하여 캡슐화를 강화하고, 강한 결합도를 방지할 수 있습니다.