"컬렉션 캡슐화하기" (Encapsulate Collection)는 객체의 컬렉션(배열, 리스트, 세트 등)에 직접 접근하는 대신, 해당 컬렉션을 반환하거나 수정하는 함수나 메서드를 통해 접근하도록 하는 리팩토링 기법입니다.

이 기법은 다음과 같은 이점을 제공합니다:

1. 컬렉션의 변경: 컬렉션을 캡슐화하면 컬렉션의 구현을 변경하더라도 이를 사용하는 코드를 변경할 필요가 없습니다. 예를 들어, 배열을 세트로 변경해야 할 경우, 이를 반환하거나 수정하는 메서드만 변경하면 됩니다.
2. 컬렉션의 유효성 검사: 컬렉션에 요소를 추가하거나 제거하는 메서드를 통해 컬렉션의 상태를 검사하고, 잘못된 상태를 방지할 수 있습니다.
3. 코드의 명확성: 컬렉션에 접근하는 방법이 명확하게 정의되어 있으므로 코드의 가독성과 유지보수성이 향상됩니다.

다음은 JavaScript에서 "컬렉션 캡슐화하기"를 적용한 예시입니다:

변경 전:

```js
class Person {
    constructor() {
        this._courses = [];
    }
}

const john = new Person();
john._courses.push('Mathematics');  // Direct access to the collection
console.log(john._courses);  // Output: ['Mathematics']
```

변경 후:

```js
class Person {
    constructor() {
        this._courses = [];
    }

    addCourse(course) {
        this._courses.push(course);
    }

    getCourses() {
        return [...this._courses];  // Return a copy to prevent modification
    }
}

const john = new Person();
john.addCourse('Mathematics');  // Access via a method
console.log(john.getCourses());  // Output: ['Mathematics']
```

변경 후의 코드에서는 `_courses` 배열에 직접 접근하는 대신 `addCourse` 메서드를 사용하여 코스를 추가하고, `getCourses` 메서드를 사용하여 코스를 가져옵니다. 이렇게 하면 컬렉션의 내부 구조를 변경하더라도 `Person` 클래스를 사용하는 코드를 변경할 필요가 없게 됩니다. 또한, `getCourses` 메서드에서는 컬렉션의 복사본을 반환하여 컬렉션의 불필요한 변경을 방지합니다.