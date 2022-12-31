<!--info-header-start--><h1>Exclude <img src="https://img.shields.io/badge/-%EC%89%AC%EC%9B%80-7aad0c" alt="쉬움"/> <img src="https://img.shields.io/badge/-%23built--in-999" alt="#built-in"/> <img src="https://img.shields.io/badge/-%23union-999" alt="#union"/></h1><blockquote><p>by Zheeeng <a href="https://github.com/zheeeng" target="_blank">@zheeeng</a></p></blockquote><p><a href="https://tsch.js.org/43/play/ko" target="_blank"><img src="https://img.shields.io/badge/-%EB%8F%84%EC%A0%84%ED%95%98%EA%B8%B0-3178c6?logo=typescript&logoColor=white" alt="도전하기"/></a> &nbsp;&nbsp;&nbsp;<a href="./README.md" target="_blank"><img src="https://img.shields.io/badge/-English-gray" alt="English"/></a>  <a href="./README.zh-CN.md" target="_blank"><img src="https://img.shields.io/badge/-%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-gray" alt="简体中文"/></a>  <a href="./README.ja.md" target="_blank"><img src="https://img.shields.io/badge/-%E6%97%A5%E6%9C%AC%E8%AA%9E-gray" alt="日本語"/></a> </p><!--info-header-end-->

`T`에서 `U`에 할당할 수 있는 타입을 제외하는 내장 제네릭 `Exclude<T, U>`를 이를 사용하지 않고 구현하세요.

### My Solutions

```ts
// solution
type MyExclude<T, U> = T extends U ? never : T;
```

```ts
// to make this work
type cases = [
  Expect<Equal<MyExclude<'a' | 'b' | 'c', 'a'>, 'b' | 'c'>>,
  Expect<Equal<MyExclude<'a' | 'b' | 'c', 'a' | 'b'>, 'c'>>,
  Expect<
    Equal<MyExclude<string | number | (() => void), Function>, string | number>
  >
];
```

### Explain

타입스크립트에서 조건부 형식을 사용할 때, `T extends U` extends를 활용해서 왼쪽 타입이 오른쪽 타입에 할당할 수 있는 지 여부를 확인하기도 한다.

```ts
T extends U ? X : Y
```

```ts
// 조건부 타입
SomeType extends OtherType ? TrueType : FalseType;

// example
type NameOrId<T extends number | string> = T extends number
  ? IdLabel
  : NameLabel;
```

- `extends`를 기준으로 왼쪽에 있는 타입이 오른쪽 타입에 할당할 수 있다면 첫 번째 분기(“참”값 분기)를, 그렇지 않다면 뒤의 분기(“거짓”값 분기)를 얻게 됩니다.

- 참고링크: https://www.typescriptlang.org/ko/docs/handbook/2/conditional-types.html

- Omit과의 비교

  - Exclude: **어떤 타입**에서 특정한 타입을 제외
  - Omit: **어떤 객체유형 타입**에서 특정 프로퍼티 제외
    ```ts
    type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;
    ```
