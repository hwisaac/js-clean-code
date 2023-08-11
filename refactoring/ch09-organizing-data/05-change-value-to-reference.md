"값을 참조로 바꾸기(Change Value to Reference)"는 객체 지향 프로그래밍에서 사용하는 리팩토링 기법 중 하나입니다. 이 기법은 객체가 값으로 다루어지는 대신, 객체에 대한 참조를 사용하는 방식으로 변경하는 것을 말합니다.

이 리팩토링 기법은 특히나 동일한 객체가 여러 곳에서 재사용되어야 하거나, 객체 간의 동일성(identity)이 중요한 경우에 유용합니다.

예를 들어, 다음과 같이 `'Customer'` 클래스가 있다고 가정해봅시다.

```js
class Order {
    constructor(data) {
        this.customer = new Customer(data.customer); // Create a new Customer
    }
}

class Customer {
    constructor(name) {
        this.name = name;
    }
}
```

위의 코드에서 `'Order'`의 생성자는 매번 새로운 `'Customer'` 객체를 생성합니다. 이는 만약 여러 `'Order'`가 동일한 `'Customer'`를 참조해야 하는 경우에 문제가 될 수 있습니다.

"값을 참조로 바꾸기"를 적용하면, 이런 문제를 해결할 수 있습니다. 예를 들어, 공유 `'Customer'` 객체를 관리하는 레지스트리를 도입할 수 있습니다.

```js
class Order {
    constructor(data) {
        this.customer = customerRegistry.register(data.customer); // Get a shared Customer
    }
}

class Customer {
    constructor(name) {
        this.name = name;
    }
}

class CustomerRegistry {
    constructor() {
        this.customers = {};
    }

    register(name) {
        if (!this.customers[name]) {
            this.customers[name] = new Customer(name);
        }
        return this.customers[name];
    }
}

const customerRegistry = new CustomerRegistry();
```

이제 `'Order'`는 동일한 `'Customer'` 이름으로 여러 번 생성된 경우, 동일한 `'Customer'` 객체를 공유하게 됩니다. 이는 메모리 사용량을 줄이는 데 도움이 될 뿐만 아니라, 객체 동일성이 중요한 경우에도 유용합니다.

다만 이 기법을 적용할 때는 주의가 필요합니다. 공유 객체의 상태가 변경될 경우, 그 변경이 모든 참조하는 곳에 영향을 미칠 수 있습니다. 따라서, 가능하다면 불변 객체를 사용하는 것이 좋습니다. 또한, 레지스트리 등을 통해 객체를 관리하는 경우, 메모리 누수를 주의해야 합니다.