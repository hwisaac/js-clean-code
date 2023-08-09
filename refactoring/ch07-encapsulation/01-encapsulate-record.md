"레코드 캡슐화하기" (Encapsulate Record)는 일반적으로 데이터를 저장하는 데 사용되는 특정 구조(예를 들어, 객체, 딕셔너리, 해시 등)에 직접 접근하는 대신, 해당 데이터에 접근하거나 변경하는 데 필요한 함수 또는 메서드를 통해 접근하는 리팩토링 기법입니다.

레코드 캡슐화는 다음과 같은 이점을 제공합니다:

1. 데이터 구조의 변경: 레코드를 캡슐화하면 데이터 구조를 변경하더라도 해당 변경이 프로그램의 다른 부분에 영향을 미치지 않습니다. 데이터를 조작하는 모든 로직이 캡슐화된 함수 또는 메서드 내에 있기 때문입니다.
2. 유효성 검사: 레코드를 변경하는 메서드를 통해 데이터의 유효성을 검사하고, 잘못된 데이터를 레코드에 추가하는 것을 방지할 수 있습니다.
3. 코드의 명확성: 데이터에 접근하는 방법이 명확하게 정의되어 있으므로 코드의 가독성과 유지보수성이 향상됩니다.

다음은 JavaScript에서 "레코드 캡슐화하기"를 적용한 예시입니다:

변경 전:

```js
let employee = {
    firstName: 'John',
    lastName: 'Doe'
};

console.log(employee.firstName);  // Output: John
```

변경 후:

```js
class Employee {
    constructor(firstName, lastName) {
        this._firstName = firstName;
        this._lastName = lastName;
    }

    getFirstName() {
        return this._firstName;
    }

    getLastName() {
        return this._lastName;
    }
}

let employee = new Employee('John', 'Doe');
console.log(employee.getFirstName());  // Output: John
```

변경 후의 코드에서는 `Employee` 클래스를 만들고, 레코드의 각 필드에 대한 getter 메서드를 추가했습니다. 이제 `employee`의 세부 사항은 직접적으로 접근하는 대신, `getFirstName`과 `getLastName` 메서드를 통해 접근할 수 있습니다. 이렇게 하면 레코드의 내부 구조를 변경하더라도 이를 사용하는 코드를 변경할 필요가 없게 됩니다. 또한 필요하다면 setter 메서드를 추가하여 데이터의 유효성을 검사할 수도 있습니다.