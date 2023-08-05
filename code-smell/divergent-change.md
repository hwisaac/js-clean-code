> 뒤엉킨 변경(Divergent Change) 악취는 하나의 클래스가 여러 개의 서로 다른 변경 사항을 처리해야 하는 상황을 의미합니다. 즉, 하나의 클래스에 여러 개의 변경 사항이 뒤엉쳐져서 발생하는 경우를 말합니다.

뒤엉킨 변경 악취는 소프트웨어의 설계가 좋지 않거나, 클래스의 역할과 책임이 모호하게 정의되어 있을 때 발생할 수 있습니다. 하나의 클래스가 여러 기능을 담당하면서 서로 다른 변경 사항에 대응해야 하는 경우, 해당 클래스를 변경해야 하는 상황에서 다른 기능에 영향을 미칠 수 있으며, 결과적으로 코드 변경이 까다로워지고 버그가 발생할 가능성이 높아집니다.

뒤엉킨 변경 악취를 해결하기 위해서는 단일 책임 원칙(Single Responsibility Principle)을 따르고, 클래스의 역할을 명확하게 분리하는 리팩토링을 수행해야 합니다. 각 클래스는 한 가지 역할만 담당하도록 설계하고, 서로 다른 변경 사항이 뒤엉키지 않도록 클래스를 적절히 분리하여야 합니다.

예를 들어, 뒤엉킨 변경 악취를 가진 코드를 살펴보겠습니다:

```js
class Order {
  constructor(orderId, customer, products) {
    this.orderId = orderId;
    this.customer = customer;
    this.products = products;
  }

  calculateTotalPrice() {
    let totalPrice = 0;
    for (const product of this.products) {
      totalPrice += product.price;
    }
    return totalPrice;
  }

  saveOrderToDatabase() {
    // 주문 정보를 데이터베이스에 저장하는 로직
  }

  sendConfirmationEmail() {
    // 주문자에게 주문 확인 이메일을 보내는 로직
  }
}
```

위의 예시에서 `Order` 클래스는 주문 정보를 저장하고, 총 주문 가격을 계산하며, 주문 정보를 데이터베이스에 저장하고, 주문자에게 이메일을 보내는 기능을 모두 포함하고 있습니다. 이로 인해 한 가지 변경이 다른 기능에도 영향을 미칠 수 있고, 코드를 수정하거나 유지 보수하기 어려워집니다.

뒤엉킨 변경 악취를 해결하기 위해 기능들을 적절히 분리하여 별도의 클래스로 만들어주는 것이 좋습니다:

```js
class Order {
  constructor(orderId, customer, products) {
    this.orderId = orderId;
    this.customer = customer;
    this.products = products;
  }

  calculateTotalPrice() {
    let totalPrice = 0;
    for (const product of this.products) {
      totalPrice += product.price;
    }
    return totalPrice;
  }
}

class OrderRepository {
  saveOrderToDatabase(order) {
    // 주문 정보를 데이터베이스에 저장하는 로직
  }
}

class OrderEmailService {
  sendConfirmationEmail(order) {
    // 주문자에게 주문 확인 이메일을 보내는 로직
  }
}
```

위의 예시에서 `Order` 클래스는 주문 정보와 주문 가격 계산에만 집중하고, 데이터베이스 저장 기능은 `OrderRepository` 클래스로, 이메일 전송 기능은 `OrderEmailService` 클래스로 분리하였습니다. 이렇게 함으로써 뒤엉킨 변경 악취를 해결하고, 클래스의 역할과 책임을 명확하게 분리하여 코드의 가독성과 유지 보수성을 향상시킬 수 있습니다.