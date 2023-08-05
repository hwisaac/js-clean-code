> 데이터 클래스(Data Class) 악취는 소프트웨어 개발에서 발생하는 코드의 특정 문제점을 가리키는 리팩토링 용어입니다. 이 악취는 주로 객체 지향 프로그래밍에서 발생하며, **클래스가 주로 데이터를 저장하고 접근하는 역할만 수행하고, 별다른 기능이 거의 없는 경우**를 가리킵니다. 즉, 클래스가 데이터만을 관리하는 용도로 사용되며, 별다른 비즈니스 로직이나 메서드가 없는 경우를 말합니다.

데이터 클래스 악취는 객체 지향 프로그래밍의 기본 원칙 중 하나인 단일 책임 원칙(Single Responsibility Principle)을 어기는 경우로 볼 수 있습니다. 클래스는 하나의 책임만을 가져야 하지만, 데이터 클래스는 단순히 데이터를 저장하거나 접근하기 위한 용도로 사용되어, 클래스의 책임이 너무 적어지게 됩니다.

데이터 클래스 악취는 코드의 중복성을 증가시키고, 가독성과 유지 보수성을 저하시키는 원인이 됩니다. 데이터 클래스는 주로 getter와 setter 메서드로만 이루어지며, 실제 비즈니스 로직은 다른 클래스에 존재하게 됩니다. 이로 인해 클래스 간의 의존성이 높아지고, 유지 보수가 어려워집니다.

데이터 클래스 악취를 해결하기 위해 주로 데이터와 기능을 함께 포함하는 클래스로 리팩토링하는 것이 좋습니다. 데이터와 기능을 한 곳에 모으면 클래스 간의 의존성이 감소하고, 코드의 가독성과 유지 보수성이 향상됩니다.

예를 들어, 데이터 클래스 악취를 가진 코드를 살펴보겠습니다:

```js
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  getWidth() {
    return this.width;
  }

  setWidth(width) {
    this.width = width;
  }

  getHeight() {
    return this.height;
  }

  setHeight(height) {
    this.height = height;
  }
}

const rectangle = new Rectangle(5, 10);
console.log(`Width: ${rectangle.getWidth()}`);
console.log(`Height: ${rectangle.getHeight()}`);
```

위의 예시에서 `Rectangle` 클래스는 주로 데이터를 저장하고 getter와 setter 메서드를 제공하는 데이터 클래스입니다. 하지만 실제로 비즈니스 로직은 `Rectangle` 클래스에 포함되어 있지 않고, 다른 클래스에서 처리해야 하는 경우가 많습니다.

데이터 클래스 악취를 해결하기 위해 데이터와 기능을 함께 포함하는 클래스로 리팩토링할 수 있습니다:

```js
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  getArea() {
    return this.width * this.height;
  }
}

const rectangle = new Rectangle(5, 10);
console.log(`Width: ${rectangle.width}`);
console.log(`Height: ${rectangle.height}`);
console.log(`Area: ${rectangle.getArea()}`);
```

위의 예시에서 `Rectangle` 클래스는 데이터와 기능을 함께 포함하도록 리팩토링되었습니다. `getWidth`와 `getHeight` 메서드 대신에 직접 `width`와 `height` 속성을 접근하고, `getArea` 메서드를 추가하여 넓이를 계산하는 기능을 클래스 내부에 포함하였습니다. 이렇게 함으로써 데이터 클래스 악취를 해결하고, 클래스의 가독성과 유지 보수성이 향상됩니다.