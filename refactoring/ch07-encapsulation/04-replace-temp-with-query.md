"임시 변수를 질의 함수로 바꾸기" (Replace Temp with Query)는 특정 값을 저장하는 데 사용되는 임시 변수를 함수 호출로 대체하는 리팩토링 기법입니다. 이 기법은 주로 반복적으로 사용되는 표현식이 있을 때 유용하며, 이를 통해 코드의 중복을 줄이고 가독성을 향상시킬 수 있습니다.

이 기법을 사용하면 코드가 더욱 선언적으로 바뀌며, 로직을 이해하고 디버깅하기 더 쉬워집니다. 또한 함수로 분리하면 재사용이 용이하고 테스트하기도 쉽습니다.

다음은 JavaScript에서 "임시 변수를 질의 함수로 바꾸기"를 적용한 예시입니다:

**변경 전:**

```
class Order {
    constructor(quantity, itemPrice) {
        this.quantity = quantity;
        this.itemPrice = itemPrice;
    }

    calculateTotal() {
        let basePrice = this.quantity * this.itemPrice;
        let discount;
        if (basePrice > 1000) 
            discount = basePrice * 0.05;
        else 
            discount = basePrice * 0.02;
        return basePrice - discount;
    }
}
```

**변경 후:**

```
class Order {
    constructor(quantity, itemPrice) {
        this.quantity = quantity;
        this.itemPrice = itemPrice;
    }

    calculateTotal() {
        return this.basePrice() - this.discount();
    }

    basePrice() {
        return this.quantity * this.itemPrice;
    }

    discount() {
        if (this.basePrice() > 1000)
            return this.basePrice() * 0.05;
        else 
            return this.basePrice() * 0.02;
    }
}
```

변경 후의 코드에서는 `basePrice`와 `discount`라는 두 개의 질의 함수를 도입했습니다. 이를 통해 `calculateTotal` 메서드가 더욱 단순해졌고, `basePrice`와 `discount` 계산 로직을 별도의 메서드로 분리하여 코드의 가독성을 향상시켰습니다. 또한 이 메서드들을 필요에 따라 재사용할 수 있습니다.

ES6+ 문법을 사용하여 "임시 변수를 질의 함수로 바꾸기" (Replace Temp with Query)를 적용해 보겠습니다. ES6+에서는 화살표 함수와 클래스 문법을 사용할 수 있어서, 위의 예시를 조금 더 간결하게 표현할 수 있습니다.

다음은 JavaScript **ES6+**에서 "임시 변수를 질의 함수로 바꾸기"를 적용한 예시입니다:

**변경 후:**

```js
class Order {
    constructor(quantity, itemPrice) {
        this.quantity = quantity;
        this.itemPrice = itemPrice;
    }

    basePrice = () => this.quantity * this.itemPrice;

    discountFactor = () => this.basePrice() > 1000 ? 0.05 : 0.02;

    discount = () => this.basePrice() * this.discountFactor();

    calculateTotal = () => this.basePrice() - this.discount();
}
```

변경 후의 코드에서는 클래스 필드와 화살표 함수를 사용하여 각 계산을 별도의 함수로 분리했습니다. 이를 통해 `calculateTotal` 함수가 더욱 단순해졌고, 각 계산에 대한 로직을 재사용하고 테스트하기가 더 쉬워졌습니다. 또한 화살표 함수는 `this` 바인딩이 자동으로 되므로, 별도의 `this` 바인딩을 신경 쓸 필요가 없습니다.