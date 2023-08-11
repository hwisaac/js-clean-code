"참조를 값으로 바꾸기(Change Reference to Value)"는 객체 지향 프로그래밍에 사용되는 리팩토링 기법 중 하나입니다. 이 기법은 참조 객체(다른 객체에 대한 참조를 저장하는 객체)를 사용하는 대신 값을 직접 저장하는 방식으로 변경합니다.

이 리팩토링 기법은 프로그램의 복잡성을 줄이고, 상태 변경에 따른 부작용을 방지하는 데 도움이 될 수 있습니다. 불변 객체(Immutable Object)를 사용하여 프로그램의 안정성을 높이는 것이 목표입니다.

다음과 같은 상황을 생각해 보겠습니다. 우리는 사용자의 도시에 대한 정보를 다루는 코드를 작성하고 있습니다.

```js
class User {
    constructor(name, city) {
        this.name = name;
        this.city = city; // Reference to a City object
    }
}

class City {
    constructor(name, country) {
        this.name = name;
        this.country = country;
    }
}
```

여기서 `User` 클래스의 `city` 필드는 `City` 객체에 대한 참조를 가지고 있습니다. 만약 `City` 객체의 상태가 바뀌면 `User`의 상태 역시 영향을 받게 됩니다.

이제 "참조를 값으로 바꾸기"를 적용해 봅시다.

```js
class User {
    constructor(name, city) {
        this.name = name;
        this.city = city.name; // Store the city's name directly
    }
}

class City {
    constructor(name, country) {
        this.name = name;
        this.country = country;
    }
}
```

`User`의 `city` 필드는 이제 `City` 객체의 참조 대신 그 객체의 `name` 필드의 값을 직접 저장하게 됩니다. 이렇게 하면 `City` 객체의 변경이 `User` 객체에 영향을 미치지 않게 됩니다. 이는 프로그램의 복잡성을 줄이고, 상태 관리를 더 간단하게 만드는 방법이 될 수 있습니다.

다만 모든 상황에서 "참조를 값으로 바꾸기"가 유용한 것은 아니며, 상황에 따라 적절히 판단해야 합니다. 객체 간의 관계, 도메인의 특성, 그리고 성능 등을 고려해야 합니다.