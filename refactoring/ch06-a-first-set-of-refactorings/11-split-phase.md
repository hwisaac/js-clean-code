"단계 쪼개기" (Split Phase)는 복잡한 과정을 더 작은 단계로 나누는 리팩토링 기법입니다. 하나의 함수나 메서드가 여러 가지 일을 동시에 처리하고 있을 때, 이를 여러 개의 독립적인 단계로 분리하여 코드의 복잡성을 줄이고 가독성을 높이는 데 사용됩니다.

이 기법을 사용하면 다음과 같은 이점이 있습니다:

1. 코드의 가독성과 이해성을 향상시킬 수 있습니다. 각 단계는 독립적이므로 각 단계를 이해하는 데 필요한 문맥(context)이 줄어듭니다.
2. 코드의 재사용성을 높일 수 있습니다. 각 단계를 독립적인 함수나 메서드로 분리하면 다른 곳에서도 이를 재사용하기 쉬워집니다.
3. 코드의 유지보수를 용이하게 할 수 있습니다. 하나의 단계가 수정되어도 다른 단계에는 영향을 미치지 않습니다.

다음은 JavaScript에서 "단계 쪼개기"를 적용한 예시입니다:

변경 전의 코드에서는 함수가 두 가지 역할을 수행하고 있습니다: 문자열로부터 숫자를 추출하고, 이 숫자를 두 배로 만듭니다.

```js
function extractAndDouble(str) {
    let num = str.match(/\d+/)[0]; // 숫자 추출
    num = Number(num) * 2; // 2배로
    return num;
}

console.log(extractAndDouble("Your number is 5"));  // Output: 10
```

이 함수를 두 단계로 나눌 수 있습니다: 하나는 문자열에서 숫자를 추출하고, 다른 하나는 숫자를 두 배로 만듭니다.

```js
function extractNumber(str) {
    return Number(str.match(/\d+/)[0]);
}

function doubleNumber(num) {
    return num * 2;
}

const num = extractNumber("Your number is 5");
console.log(doubleNumber(num));  // Output: 10
```

이제 각 단계는 명확하고 독립적입니다. 각 함수는 하나의 일을 수행하므로 코드의 가독성이 높아지고, 필요에 따라 각 함수를 별도로 재사용할 수 있게 되었습니다.