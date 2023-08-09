"필드 옮기기(Move Field)"는 특정 필드(속성)가 자신이 속한 클래스보다 다른 클래스와 더 강하게 연관되어 있는 경우, 해당 필드를 다른 클래스로 이동시키는 리팩토링 기법입니다.

이 기법은 객체 지향 프로그래밍에서 캡슐화, 응집도, 결합도 등의 원칙을 더 잘 적용하기 위해 사용됩니다. "필드 옮기기"를 통해 클래스의 책임을 더욱 명확히 분리하고, 코드의 유지보수성과 가독성을 높일 수 있습니다.

다음은 이 리팩토링 기법을 적용하기 전과 후의 예제입니다.

**적용 전**:

```js
class Customer {
    constructor(discountRate) {
        this.discountRate = discountRate;
    }

    applyDiscount(price) {
        return price * (1 - this.discountRate);
    }
}

class Order {
    constructor(price, customer) {
        this.price = price;
        this.customer = customer;
    }

    getDiscountedPrice() {
        return this.customer.applyDiscount(this.price);
    }
}
```

위 코드에서 `Customer` 클래스의 `applyDiscount` 메소드는 `Order` 클래스의 `price`를 이용합니다. 이처럼 `Customer`가 `Order`의 정보를 필요로 하는 경우, `Customer`에 속한 `discountRate`를 `Order` 클래스로 옮기는 것이 적절할 수 있습니다.

**적용 후**:

```js
class Customer {}

class Order {
    constructor(price, discountRate) {
        this.price = price;
        this.discountRate = discountRate;
    }

    applyDiscount() {
        return this.price * (1 - this.discountRate);
    }
}
```

`Order` 클래스는 이제 `applyDiscount` 메소드를 직접 가지고 있으며, 이를 수행하는 데 필요한 모든 데이터도 가지고 있습니다. 이처럼 "필드 옮기기"를 통해 코드의 응집도를 높이고 결합도를 줄일 수 있습니다.