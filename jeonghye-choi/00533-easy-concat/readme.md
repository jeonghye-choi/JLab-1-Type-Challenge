<!--info-header-start--><h1>Concat <img src="https://img.shields.io/badge/-%EC%89%AC%EC%9B%80-7aad0c" alt="쉬움"/> <img src="https://img.shields.io/badge/-%23array-999" alt="#array"/></h1><blockquote><p>by Andrey Krasovsky <a href="https://github.com/bre30kra69cs" target="_blank">@bre30kra69cs</a></p></blockquote><p><a href="https://tsch.js.org/533/play/ko" target="_blank"><img src="https://img.shields.io/badge/-%EB%8F%84%EC%A0%84%ED%95%98%EA%B8%B0-3178c6?logo=typescript&logoColor=white" alt="도전하기"/></a> &nbsp;&nbsp;&nbsp;<a href="./README.md" target="_blank"><img src="https://img.shields.io/badge/-English-gray" alt="English"/></a>  <a href="./README.zh-CN.md" target="_blank"><img src="https://img.shields.io/badge/-%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-gray" alt="简体中文"/></a>  <a href="./README.ja.md" target="_blank"><img src="https://img.shields.io/badge/-%E6%97%A5%E6%9C%AC%E8%AA%9E-gray" alt="日本語"/></a> </p><!--info-header-end-->

JavaScript의 `Array.concat` 함수를 타입 시스템에서 구현하세요. 타입은 두 인수를 받고, 인수를 왼쪽부터 concat한 새로운 배열을 반환해야 합니다.

### My Solutions

```ts
// solution
type Concat<T extends Array<any>, U extends Array<any>> = [...T, ...U];
```

```ts
// to make this work
import type { Equal, Expect } from '@type-challenges/utils';

type cases = [
  Expect<Equal<Concat<[], []>, []>>,
  Expect<Equal<Concat<[], [1]>, [1]>>,
  Expect<Equal<Concat<[1, 2], [3, 4]>, [1, 2, 3, 4]>>,
  Expect<
    Equal<
      Concat<['1', 2, '3'], [false, boolean, '4']>,
      ['1', 2, '3', false, boolean, '4']
    >
  >
];
```

### Explain

- input으로 들어오는 T와 U의 타입 모두 array이여야 한다.
- spread operator를 사용

  spread operator는 array의 요소들을 쪼개서 개별요소로 리턴해준다.

  ```ts
  // example
  const arr1 = [1, 2, 3];
  console.log(...arr1); // 1, 2, 3
  ```
