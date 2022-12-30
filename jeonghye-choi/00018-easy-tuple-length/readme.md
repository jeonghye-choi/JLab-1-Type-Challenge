<!--info-header-start--><h1>Length of Tuple <img src="https://img.shields.io/badge/-%EC%89%AC%EC%9B%80-7aad0c" alt="쉬움"/> <img src="https://img.shields.io/badge/-%23tuple-999" alt="#tuple"/></h1><blockquote><p>by sinoon <a href="https://github.com/sinoon" target="_blank">@sinoon</a></p></blockquote><p><a href="https://tsch.js.org/18/play/ko" target="_blank"><img src="https://img.shields.io/badge/-%EB%8F%84%EC%A0%84%ED%95%98%EA%B8%B0-3178c6?logo=typescript&logoColor=white" alt="도전하기"/></a> &nbsp;&nbsp;&nbsp;<a href="./README.md" target="_blank"><img src="https://img.shields.io/badge/-English-gray" alt="English"/></a>  <a href="./README.zh-CN.md" target="_blank"><img src="https://img.shields.io/badge/-%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-gray" alt="简体中文"/></a>  <a href="./README.ja.md" target="_blank"><img src="https://img.shields.io/badge/-%E6%97%A5%E6%9C%AC%E8%AA%9E-gray" alt="日本語"/></a> </p><!--info-header-end-->

배열(튜플)을 받아 길이를 반환하는 제네릭 `Length<T>`를 구현하세요.

### My Solutions

```ts
// solution
type Length<T extends readonly any[]> = T['length'];
```

```ts
// to make this work
const tesla = ['tesla', 'model 3', 'model X', 'model Y'] as const;
const spaceX = [
  'FALCON 9',
  'FALCON HEAVY',
  'DRAGON',
  'STARSHIP',
  'HUMAN SPACEFLIGHT',
] as const;

type cases = [
  Expect<Equal<Length<typeof tesla>, 4>>,
  Expect<Equal<Length<typeof spaceX>, 5>>,
  // @ts-expect-error
  Length<5>,
  // @ts-expect-error
  Length<'hello world'>
];
```

### Explain

T의 길이를 알고 싶을 때는 `T['length']`를 사용한다.

- https://www.typescriptlang.org/docs/handbook/2/objects.html#tuple-types

- 질문

  - 아래 방법이 안되는 이유

    ```ts
    type Length<T extends { length: number }> = T['length'];
    ```

    위 case 중에서 `Length<'hello world'>`에 대해 error를 return 하지 않기 때문이다.
    왜냐하면 'hello world'라는 string 타입에 대해 length를 구할 수 있기 때문이다.

    ```ts
    'hello world'.length; //4
    ```
