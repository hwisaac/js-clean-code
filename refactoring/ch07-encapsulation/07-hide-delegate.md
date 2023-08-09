"위임 숨기기(Hide Delegate)"라는 용어는 리팩토링, 즉 코드의 구조를 개선하는 과정에서 사용됩니다. 위임 숨기기는 객체의 속성이나 메소드가 다른 객체에 위임될 때, 이를 호출하는 클라이언트 코드가 그 위임을 직접 알고 있는 상태를 방지하는 것을 목적으로 합니다.

위임 숨기기를 사용함으로써 클라이언트 코드는 직접적인 위임을 알 필요 없이 메소드를 호출하게 되므로, 클라이언트 코드와 위임 대상 객체 사이의 결합도를 줄일 수 있습니다.

예를 들어, 다음과 같은 JavaScript 코드가 있다고 해봅시다:

```js
class Department {
    constructor(manager) {
        this.manager = manager;
    }
}

class Person {
    constructor(department) {
        this.department = department;
    }
}

const john = new Person(new Department('Michael'));
console.log(john.department.manager); // 'Michael'
```

이 경우 `Person` 객체를 사용하는 클라이언트 코드는 `Person` 객체의 `Department` 객체에 직접 접근하여 매니저를 찾아야 합니다. 따라서 `Person`과 `Department` 사이에 강한 결합이 생깁니다.

위임 숨기기 리팩토링을 적용하면 다음과 같이 변합니다:

```js
class Department {
    constructor(manager) {
        this.manager = manager;
    }
}

class Person {
    constructor(department) {
        this.department = department;
    }
  
    getManager() {
        return this.department.manager;
    }
}

const john = new Person(new Department('Michael'));
console.log(john.getManager()); // 'Michael'
```

`Person` 클래스에 `getManager` 메소드를 추가함으로써, 클라이언트 코드는 `Person` 객체를 통해 간접적으로 매니저 정보에 접근할 수 있게 되었습니다. 이렇게 함으로써 `Person`과 `Department` 사이의 결합도가 낮아지고 코드의 유지보수성이 향상됩니다.