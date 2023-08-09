"클래스 추출하기" (Extract Class)는 소프트웨어 리팩토링의 한 기법으로, 하나의 클래스가 너무 많은 역할을 수행하거나 관련성이 높은 여러 속성 및 메서드가 있을 때 새로운 클래스로 분리하는 것을 말합니다. 이 기법을 통해 각 클래스의 책임을 분명하게 하고 코드의 가독성과 유지보수성을 향상시킬 수 있습니다.

다음은 JavaScript ES6+에서 "클래스 추출하기"를 적용한 예시입니다:

**변경 전:**

```js
class Person {
    constructor(name, street, city, state, telephone, email) {
        this.name = name;
        this.street = street;
        this.city = city;
        this.state = state;
        this.telephone = telephone;
        this.email = email;
    }

    getContactInfo() {
        return `Tel: ${this.telephone}, Email: ${this.email}`;
    }
}

const john = new Person("John Doe", "123 Street", "City", "State", "123-456-7890", "john@example.com");
console.log(john.getContactInfo());
```

**변경 후:**

```js
class Contact {
    constructor(telephone, email) {
        this.telephone = telephone;
        this.email = email;
    }

    getContactInfo() {
        return `Tel: ${this.telephone}, Email: ${this.email}`;
    }
}

class Person {
    constructor(name, street, city, state, contact) {
        this.name = name;
        this.street = street;
        this.city = city;
        this.state = state;
        this.contact = contact;
    }
}

const johnContact = new Contact("123-456-7890", "john@example.com");
const john = new Person("John Doe", "123 Street", "City", "State", johnContact);

console.log(john.contact.getContactInfo());
```

변경 후의 코드에서는 연락처 정보를 관리하는 새로운 `Contact` 클래스를 생성하였습니다. 이를 통해 `Person` 클래스의 책임을 줄이고, 각 클래스가 관리하는 정보를 명확하게 하였습니다. 또한 연락처 관련 정보와 기능을 재사용하고 테스트하기 쉬운 `Contact` 클래스를 별도로 가짐으로써 코드의 유지보수성을 향상시켰습니다.