기능 편애(Feature Envy) 악취는 소프트웨어 개발에서 발생하는 코드의 특정 문제점을 가리키는 리팩토링 용어입니다. 이 악취는 메서드가 자신이 속한 클래스보다 다른 클래스의 기능을 너무 많이 호출하거나 사용하는 경우를 가리킵니다. 즉, 어떤 메서드가 자신이 속한 클래스보다 다른 클래스의 데이터나 기능에 "너무 집착"하여 다른 클래스와 밀접한 관계를 가지게 되는 것을 의미합니다.

기능 편애는 객체 지향 프로그래밍의 기본 원칙 중 하나인 정보 은닉(Encapsulation) 원칙을 어기는 상황으로 볼 수 있습니다. 메서드가 다른 클래스의 데이터에 너무 의존적이라면 해당 기능을 더 적절한 클래스로 이동시키는 것이 좋습니다. 이렇게 함으로써 코드의 의존성을 최소화하고, 더 응집도 있는(cohesive) 클래스를 유지할 수 있습니다.

기능 편애 악취를 해결하는 방법은 주로 메서드를 다른 클래스로 이동하거나, 새로운 클래스를 생성하여 기능을 적절히 분배하는 리팩토링을 수행하는 것입니다. 이렇게 함으로써 클래스 간의 의존성이 낮아지고, 코드의 가독성과 유지 보수성이 향상됩니다.

예를 들어, 기능 편애 악취를 가진 코드를 살펴보겠습니다:

```js
class Order {
  constructor(orderId, customer) {
    this.orderId = orderId;
    this.customer = customer;
  }

  calculateTotalPrice() {
    let totalPrice = 0;
    for (const item of this.customer.shoppingCart.items) {
      totalPrice += item.price;
    }
    return totalPrice;
  }
}

class Customer {
  constructor(name) {
    this.name = name;
    this.shoppingCart = new ShoppingCart();
  }
}

class ShoppingCart {
  constructor() {
    this.items = [];
  }
}
```

위의 예시에서 `Order` 클래스의 `calculateTotalPrice` 메서드는 `Customer` 클래스의 `shoppingCart`를 너무 많이 호출하고 사용하고 있습니다. 이로 인해 `Order` 클래스가 `Customer` 클래스에 대한 기능에 너무 편애되어 있으며, 의존성이 높아집니다.

기능 편애 악취를 해결하기 위해 `calculateTotalPrice` 메서드를 `Customer` 클래스로 이동시키거나, 새로운 클래스를 생성하여 `calculateTotalPrice` 기능을 분리하는 것이 좋습니다. 이렇게 함으로써 `Order` 클래스와 `Customer` 클래스의 의존성이 낮아지고, 더 명확하고 응집도 있는 클래스 구조를 유지할 수 있습니다.