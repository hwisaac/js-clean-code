"파생 변수를 질의 함수로 바꾸기(Replace Derived Variable with Query)"는 코드 리팩토링 기법 중 하나로, 파생 변수(즉, 다른 변수로부터 계산되어 얻어지는 변수)를 사용하는 대신에 그 값을 계산해주는 함수(질의 함수)를 사용하는 방법을 말합니다.

이 기법은 특히나 파생 변수의 값이 복잡하게 변경되는 경우에 유용합니다. 파생 변수의 값이 여러 군데에서 변경될 수 있다면, 그 변수의 값을 추적하고 관리하는 것은 어려울 수 있습니다. 이런 경우에는 파생 변수를 직접 관리하는 대신, 필요한 시점에 그 값을 계산해주는 함수를 사용하는 것이 더욱 안전하고 관리하기 쉬울 수 있습니다.

예를 들어, 아래와 같은 코드가 있다고 가정해봅시다.

```js
class Order {
    constructor(quantity, price) {
        this.quantity = quantity;
        this.price = price;
        this.totalCost = quantity * price; // Derived variable
    }

    applyDiscount(discount) {
        this.totalCost = this.totalCost * (1 - discount);
    }
}
```

위의 코드에서 `totalCost`는 파생 변수로, 수량(`quantity`)과 가격(`price`)으로부터 계산됩니다. 그런데 `applyDiscount` 메소드에서 이 값이 다시 변경되고 있습니다. 이렇게 파생 변수의 값이 여러 군데에서 변경되는 경우, 그 값을 추적하고 관리하는 것이 복잡해질 수 있습니다.

"파생 변수를 질의 함수로 바꾸기"를 적용하면 다음과 같이 바뀔 수 있습니다.

```js
class Order {
    constructor(quantity, price) {
        this.quantity = quantity;
        this.price = price;
        this.discount = 0;
    }

    get totalCost() {
        return this.quantity * this.price * (1 - this.discount);
    }

    applyDiscount(discount) {
        this.discount = discount;
    }
}
```

이제 `totalCost`는 파생 변수가 아닌 질의 함수로 바뀌었고, `applyDiscount` 메소드는 할인율(`discount`)을 직접 관리합니다. 이렇게 하면 `totalCost`의 값 추적과 관리가 더욱 단순해집니다.