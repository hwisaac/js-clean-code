"조건부 로직을 다형성으로 바꾸기(Replace Conditional with Polymorphism)"는 객체 지향 프로그래밍에서 사용하는 **리팩토링 기법 중 하나**입니다. 이 기법은 조건문을 다형성을 활용하여 각 조건에 해당하는 서브클래스를 만들고, 각각의 서브클래스에서 필요한 동작을 오버라이딩하여 구현하는 방식으로 변경하는 것을 말합니다.

이 기법은 조건부 로직을 처리하는 코드의 양을 줄이고, 유지보수를 용이하게 만들어줍니다. 또한, 코드의 확장성과 유연성을 높이는 데 도움이 됩니다.

물체의 운동을 표현하는 코드를 간단한 예시로 살펴보겠습니다. 다음과 같이 운동을 나타내는 물체 클래스가 있습니다.

```
class MovingObject {
  constructor(type, velocity) {
    this.type = type;
    this.velocity = velocity;
  }

  move() {
    if (this.type === 'car') {
      console.log(`Car is moving at a speed of ${this.velocity} km/h.`);
    } else if (this.type === 'bike') {
      console.log(`Bike is moving at a speed of ${this.velocity} km/h.`);
    } else if (this.type === 'plane') {
      console.log(`Plane is flying at a speed of ${this.velocity} km/h.`);
    } else {
      console.log(`Unknown type of object.`);
    }
  }
}
```

위 코드에서는 `move` 메소드 내에 조건부 로직이 사용되어 각 물체의 운동 방식을 출력하고 있습니다. 이를 "조건부 로직을 다형성으로 바꾸기"를 적용하여 리팩토링하면 다음과 같이 됩니다.

```
class MovingObject {
  constructor(type, velocity) {
    this.type = type;
    this.velocity = velocity;
  }

  move() {
    console.log(this.getMovementDescription());
  }

  getMovementDescription() {
    switch (this.type) {
      case 'car':
        return `Car is moving at a speed of ${this.velocity} km/h.`;
      case 'bike':
        return `Bike is moving at a speed of ${this.velocity} km/h.`;
      case 'plane':
        return `Plane is flying at a speed of ${this.velocity} km/h.`;
      default:
        return `Unknown type of object.`;
    }
  }
}
```

이제 `getMovementDescription` 메소드를 추가하여 각 물체의 운동 방식을 반환하도록 변경하였습니다. 이렇게 하면 조건부 로직이 사라지고, 각 물체의 운동 방식을 나타내는 부분이 독립적인 메소드로 분리되어 코드의 가독성과 유지보수성이 향상됩니다. 또한, 새로운 물체가 추가되더라도 해당 물체의 운동 방식을 나타내는 `getMovementDescription` 메소드만 추가하면 되므로 코드의 확장성과 유연성이 증가하게 됩니다.