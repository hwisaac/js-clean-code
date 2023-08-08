"클래스 인라인하기" (Inline Class)는 리팩토링의 한 기법으로, 한 클래스가 거의 아무 것도 하지 않고 있을 때 그 클래스의 기능을 다른 클래스로 통합하는 작업을 말합니다. 즉, 클래스가 제공하는 기능이 별로 없거나 단순히 다른 클래스에 데이터를 전달하는 역할만 수행한다면, 그 클래스는 필요 없는 복잡성을 추가하므로 인라인 처리하여 제거하는 것이 좋습니다.

다음은 JavaScript ES6+에서 "클래스 인라인하기"를 적용한 예시입니다:

**변경 전:**

```js
class TelephoneNumber {
    constructor(areaCode, number) {
        this.areaCode = areaCode;
        this.number = number;
    }

    getFullNumber() {
        return `${this.areaCode}-${this.number}`;
    }
}

class Person {
    constructor(name, telephoneNumber) {
        this.name = name;
        this.telephoneNumber = telephoneNumber;
    }
}

const johnPhone = new TelephoneNumber("123", "4567890");
const john = new Person("John Doe", johnPhone);

console.log(john.telephoneNumber.getFullNumber());  // Output: 123-4567890
```

**변경 후:**

```js
class Person {
    constructor(name, areaCode, number) {
        this.name = name;
        this.areaCode = areaCode;
        this.number = number;
    }

    getFullNumber() {
        return `${this.areaCode}-${this.number}`;
    }
}

const john = new Person("John Doe", "123", "4567890");

console.log(john.getFullNumber());  // Output: 123-4567890
```

변경 후의 코드에서는 `TelephoneNumber` 클래스의 기능을 `Person` 클래스에 직접 통합하였습니다. 이를 통해 코드의 복잡성을 줄이고 가독성을 향상시켰습니다.