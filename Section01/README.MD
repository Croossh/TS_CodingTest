# 회고

## <8번 일곱 난장이 문제>
⏩[8번 문제풀이 보러가기](https://github.com/Croossh/TS_CodingTest/blob/ea2671ec6a167639639d95968db2c85b31cc3daa/Section01/08_%EC%9D%BC%EA%B3%B1%EB%82%9C%EC%9F%81%EC%9D%B4.ts)<br>
이 문제는 `9`개의 숫자중 `7`개의 조합이 `100`이 되는 숫자 조합을 찾는 문제이다.<br>
기본 문제는 단하나의 조건만 찾으면 되는 문제였다. 하지만 **욕심이 생겨 모든 경우의 수를 찾아보고 싶었다.**~~(그래도 정답은 하나였던건 안비밀)~~<br>
그렇게 해서 경우의 수를 따지는 방법을 알아본 결과, `재귀함수` 와 `조합`을 통해 구하는 방법을 알아냈다.<br>

```ts
const getCombinations = function (
  selectArr: number[],
  selectNumber: number
  ): Array<number[]> {
    const results: Array<number[]> = [];
    // 재귀함수 탈출 조건
    if (selectNumber === 1) return selectArr.map((el) => [el]);
```

`재귀함수`는 자기자신을 무한대로 호출하는 함수이기 때문에 반드시 `탈출조건`이 있어야한다.<br>

```ts
selectArr.forEach((item: number, index: number, origin: number[]) => {
  const rest: number[] = origin.slice(index + 1);
  const combinations: Array<number[]> = getCombinations(rest, selectNumber - 1);
  const attached: Array<number[]> = combinations.map((el) => [item, ...el]);
  ...
```

`조합`을 만들기 위한 로직이다.<br> 0. 하단에서 `getCombinations`의 두번째 인자를 `7`로 주었다.

1. `rest`로 해당 `index`를 제외한 나머지 배열을 만들고
2. `getCombinations`를 다시 호출하여 `rest`배열을 하나씩 쪼갠다.(탈출조건인 selectNumber가 1이 되면 끝난다)
3. 쪼갠 배열들을 하나씩 조합한다.
4. 이후 조합한 배열들을 조건에 맞는지 검사하는 로직을 통해 답을 산출한다.
<hr>

이 외에도 Type을 지정하는데도 고민이 있었다. 숫자로 만들어진 배열은

```ts
const arr: number[] = ...
```

이와 같이 하면됐으나, 배열안에 숫자로이루어진 배열은 어떻게 설정해야하는지 몰랐다. 알게된 방법은...

```ts
const arr: number[] = ... // 속기 구문
const arr: Array<number> = ... // 일반 구문
```

```ts
// 원하는 타입
// [[1,2,3], [2,3,4], [3,4,5], ...]
const arr: Array<number[]> = ... // 응용 버젼
```

구문의 차이점이 있다는 것을 알게되었고, 일반 구문안에 응용을 함으로써 원하는 타입을 선언할 수 있게 되었다.<br>
나중에 알게된 충격적인 사실

```ts
const arr: number[][] = ...
```

이것도 가능하..다!

<hr>

## <17번 중복 단어 제거>
⏩[17번 문제풀이 보러가기](https://github.com/Croossh/TS_CodingTest/blob/ea2671ec6a167639639d95968db2c85b31cc3daa/Section01/17_%EC%A4%91%EB%B3%B5%EB%8B%A8%EC%96%B4%EC%A0%9C%EA%B1%B0.ts)<br>
```ts
const setArr = [...new Set(str)].join("");
```

중복을 없애기 위해 `Set`메서드를 이용했다. `Set` 을 처음 써봤는데, `new Set` 으로 새로운 인스턴스를 생성하면 결과 값은 `값`으로 만 이루어진 객체 `{ k, s, e, t }` 가 나오게 된다.

1. 배열 형태로 반환 받고 싶었기에 new 구문 전체를 배열에 감싸고, 스프레드 연산자를 통해 객체 안의 값들을 뽑아왔다.
2. 그 이후 `join` 메서드를 통해 `string` 형태로 반환했다.
