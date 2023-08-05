기본형 집착(Primitive Obsession) 악취는 소프트웨어 개발에서 발생하는 코드의 특정 문제점을 가리키는 리팩토링 용어입니다. 이 악취는 **프로그램에서 기본 데이터 타입(예: 숫자, 문자열)을 너무 많이 사용하여 객체를 만들지 않고, 기능을 구현하려는 경향을 가리킵니다**. 즉, 객체를 사용하지 않고 기본 데이터 타입만을 사용하여 코드를 구현하는 것을 의미합니다.

기본형 집착은 객체 지향 프로그래밍의 기본 원칙 중 하나인 객체 지향 설계(OOD) 원칙을 어기는 경우로 볼 수 있습니다. 객체 지향적으로 프로그램을 구현할 때는 기능을 객체로 추상화하고, 기능을 구현하는 데 필요한 데이터를 해당 객체의 속성으로 만들어야 합니다. 하지만 기본형 집착이 발생하면 데이터를 단순한 기본 데이터 타입으로 남겨두고, 기능을 함수 또는 메서드로만 구현하려는 경향이 생깁니다.

기본형 집착 악취를 해결하는 방법은 주로 적절한 객체를 설계하여 기본 데이터 타입을 객체로 대체하는 리팩토링을 수행하는 것입니다. 이렇게 함으로써 코드의 가독성과 유지 보수성이 향상됩니다. 또한, 데이터와 기능이 더 명확하게 구분되며, 객체 지향적인 설계를 유지할 수 있습니다.

예를 들어, 기본형 집착 악취를 가진 코드를 살펴보겠습니다:

```js
function calculateTotalPrice(price, quantity) {
  return price * quantity;
}

const productName = 'Widget';
const productPrice = 10;
const productQuantity = 3;

const totalPrice = calculateTotalPrice(productPrice, productQuantity);
console.log(`Total price of ${productName}: $${totalPrice}`);
```

위의 예시에서 `calculateTotalPrice` 함수는 기본 데이터 타입인 `price`와 `quantity`를 매개변수로 받아서 총 가격을 계산합니다. 이로 인해 데이터와 기능이 분리되지 않고, 함수를 호출하는 곳에서 매번 `price`와 `quantity`를 전달해야 합니다.

기본형 집착 악취를 해결하기 위해 `calculateTotalPrice` 함수의 매개변수를 객체로 대체하고, `Product` 클래스를 만들어 데이터와 기능을 함께 추상화하는 것이 좋습니다. 이렇게 함으로써 데이터와 기능이 함께 묶여있어 더 응집도 있는 클래스를 유지할 수 있습니다:

```js
class Product {
  constructor(name, price, quantity) {
    this.name = name;
    this.price = price;
    this.quantity = quantity;
  }

  calculateTotalPrice() {
    return this.price * this.quantity;
  }
}

const product = new Product('Widget', 10, 3);
const totalPrice = product.calculateTotalPrice();
console.log(`Total price of ${product.name}: $${totalPrice}`);
```

위의 예시에서 `calculateTotalPrice` 함수를 `Product` 클래스로 이동시켜 데이터와 기능을 함께 추상화했습니다. 이렇게 함으로써 코드의 가독성이 향상되고, 객체 지향적인 설계를 유지할 수 있게 됩니다.