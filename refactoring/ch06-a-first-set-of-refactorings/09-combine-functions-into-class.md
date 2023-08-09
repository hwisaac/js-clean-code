"여러 함수를 클래스로 묶기" (Combine Functions into Class)는 객체 지향 프로그래밍에서 흔히 사용되는 리팩토링 기법입니다. 이 기법은 서로 연관된 데이터와 함수(메서드)들을 하나의 클래스로 묶는 것을 의미합니다.

이러한 리팩토링 기법을 사용하면 다음과 같은 이점을 얻을 수 있습니다:

1. 코드의 구조를 명확하게 표현하고, 데이터와 함수의 관계를 명확히 할 수 있습니다.
2. 클래스의 인스턴스 간에 데이터를 공유하는 것이 아니라 각 인스턴스가 자신만의 상태를 갖게 되므로 코드의 안정성을 높일 수 있습니다.
3. 객체 지향 프로그래밍의 재사용, 확장성 등의 이점을 누릴 수 있습니다.

다음은 JavaScript에서 "여러 함수를 클래스로 묶기"를 적용한 예시입니다:

변경 전:

```js
let title = "";
let text = "";

function setTitle(newTitle) {
    title = newTitle;
}

function setText(newText) {
    text = newText;
}

function printNote() {
    console.log(`Title: ${title}`);
    console.log(`Text: ${text}`);
}
```

변경 후:

```js
class Note {
    constructor() {
        this.title = "";
        this.text = "";
    }

    setTitle(newTitle) {
        this.title = newTitle;
    }

    setText(newText) {
        this.text = newText;
    }

    printNote() {
        console.log(`Title: ${this.title}`);
        console.log(`Text: ${this.text}`);
    }
}
```

변경 후의 코드에서는 `Note`라는 클래스를 만들고, `title`, `text`라는 속성과 `setTitle`, `setText`, `printNote`라는 메서드를 가지게 되었습니다. 이렇게 하면 각각의 `Note` 인스턴스가 자신만의 `title`과 `text`를 가지게 되므로 데이터 관리가 훨씬 쉬워집니다. 또한, 메서드와 데이터가 하나의 클래스로 묶여있으므로 코드의 가독성과 유지보수성이 향상됩니다.