"기본형을 객체로 바꾸기" (Replace Primitive with Object)는 소프트웨어 리팩토링의 한 가지 기법으로, 코드에서 기본 데이터 타입 (예를 들어, 숫자, 문자열, 불리언 등)을 사용하는 대신 이를 객체로 대체하는 것을 의미합니다. 이 리팩토링 기법은 특히 해당 데이터에 추가적인 동작이나 속성이 필요할 때 유용합니다.

예를 들어, 문자열을 사용하여 사람의 이름을 나타내는 경우가 있을 수 있습니다. 그러나 이름에 관련된 추가적인 동작 (예를 들어, 이름의 유효성 검사, 이름의 표시 형식 조정 등)이 필요한 경우, 이름을 나타내는 별도의 `Name` 객체를 만드는 것이 더 효과적일 수 있습니다.

다음은 JavaScript에서 "기본형을 객체로 바꾸기"를 적용한 예시입니다:

**변경 전:**

```js
class Person {
    constructor(name) {
        this.name = name;
    }
}

const john = new Person('John Doe');
console.log(john.name);  // Output: John Doe
```

**변경 후:**

```js
class Name {
    constructor(fullName) {
        this.fullName = fullName;
    }

    getFirstName() {
        return this.fullName.split(' ')[0];
    }

    getLastName() {
        return this.fullName.split(' ')[1];
    }
}

class Person {
    constructor(name) {
        this.name = new Name(name);
    }
}

const john = new Person('John Doe');
console.log(john.name.getFirstName());  // Output: John
console.log(john.name.getLastName());   // Output: Doe
```

변경 후의 코드에서는 `Name` 객체를 도입하여 이름에 관련된 추가적인 동작을 제공하였습니다. 이제 `Person` 객체를 사용하는 코드에서는 이름의 성과 이름을 개별적으로 가져올 수 있습니다. 이와 같이 기본형을 객체로 바꾸는 것은 코드의 가독성을 향상시키고, 코드의 재사용성과 유지 관리성을 높일 수 있습니다.