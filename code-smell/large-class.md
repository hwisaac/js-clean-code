Large Class 악취는 소프트웨어 개발에서 발생하는 코드의 특정 문제점을 가리키는 리팩토링 용어입니다. 이 악취는 하나의 클래스가 너무 많은 책임을 지고 있거나, 너무 많은 속성과 메서드를 가지고 있어서 클래스가 복잡하고 장황해지는 상황을 가리킵니다.

Large Class 악취는 객체 지향 프로그래밍의 기본 원칙 중 하나인 단일 책임 원칙(Single Responsibility Principle)을 어기는 경우가 많습니다. 즉, 하나의 클래스는 하나의 책임만 가져야 합니다. Large Class는 여러 기능과 동작을 담당하다 보니 클래스의 크기가 커지고, 코드의 가독성과 유지 보수성이 저하됩니다.

Large Class 악취를 해결하는 방법은 주로 클래스의 분리와 리팩토링을 통해 이루어집니다. 클래스를 더 작은 단위로 분리하여 각 클래스가 하나의 책임만을 갖도록 만들고, 필요한 기능은 필요한 클래스에 적절히 분배하여 코드의 가독성과 유지 보수성을 개선합니다.

예를 들어, Large Class 악취를 가진 클래스를 예시로 살펴보겠습니다:

```js
class Order {
  constructor(orderId, customerName, customerAddress, items) {
    this.orderId = orderId;
    this.customerName = customerName;
    this.customerAddress = customerAddress;
    this.items = items;
  }

  calculateTotalPrice() {
    let totalPrice = 0;
    for (const item of this.items) {
      totalPrice += item.price;
    }
    return totalPrice;
  }

  generateInvoice() {
    // Invoice 생성과 관련된 복잡한 로직
  }

  validateOrder() {
    // 주문 유효성 검사와 관련된 복잡한 로직
  }

  shipOrder() {
    // 주문 배송과 관련된 복잡한 로직
  }

  // ... 많은 다른 메서드들 ...
}
```

위의 예시에서 `Order` 클래스는 주문과 관련된 여러 기능을 모두 담당하고 있습니다. 주문 생성, 가격 계산, 인보이스 생성, 유효성 검사, 주문 배송 등의 기능이 모두 하나의 클래스에 포함되어 있습니다. 이로 인해 클래스가 복잡해지고, 책임이 과도하게 집중됩니다.

Large Class 악취를 해결하기 위해 클래스를 세분화하고, 각 클래스가 단일 책임을 갖도록 리팩토링할 수 있습니다. 예를 들어, 주문 생성은 `Order` 클래스가 담당하고, 가격 계산은 `OrderCalculator` 클래스로 분리하고, 인보이스 생성은 `InvoiceGenerator` 클래스로 분리하는 등의 방법을 사용합니다. 이렇게 하면 클래스가 더 작고 간단해지며, 코드의 가독성과 유지 보수성이 향상됩니다.