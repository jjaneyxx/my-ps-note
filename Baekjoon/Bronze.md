# 11654 . 아스키코드

**문제**
```
알파벳 소문자, 대문자, 숫자 0-9중 하나가 주어졌을 때, 주어진 글자의 아스키 코드값을 출력하는 프로그램을 작성하시오.
```

**풀이**
``` jsx
// 아스키코드값 출력
// input 은 객체, input[0] 는 문자열
// 07:52

const input = require('fs').readFileSync("./input.txt").toString().split();

console.log(input[0].charCodeAt());
```

- 처음에는 `input.charCodeAt()` 을 출력하려 했는데 오류가 났다.
- `input` 은 객체이고, 내가 원하는 해당 문자열을 뽑아내려면 `input[0]` 를 써야 한다.
	- `input` 은 문자열로 이루어진 객체
- 문자를 아스키코드로 변환할 때는 `'문자열'.charCodeAt()`


🐕**아스키코드값 변환 : charCodeAt( ) 과 fromCharCode** 
- charcode 가 아스키코드

**문자 → 아스키코드**
``` js
'문자열'.charCodeAt()
```

- 문자열의 특정 인덱스에 있는 문자의 아스키코드를 반환한다. 
-  `charCodeAt( )` 은 `string` 타입에만 사용할 수 있다. 
- 그럼 `charCodeAt( )` 은 오직 하나의 문자에만 사용 가능한 걸까 ?
	- 정답은 `NO`, 문자열에도 사용할 수 있음 
	- `"hello".charCodeAt(0)` → 문자열(hello) 내 0번 인덱스(h) 의 아스키코드값으로 변환됨 (104)

**아스키코드 → 문자**
``` js
String.fromCharCode(아스키코드); 
```

- fromCharCode 는 String 의 정적 메서드이므로 String 과 함께 사용한다. 
- 마찬가지로 fromCharCode 도 인자는 `number` 타입만 가능하다. 
- 인자에 여러 숫자를 나열해서 단어도 만들 수 있다. 
  ![4qDbMUI.png|489](https://i.imgur.com/4qDbMUI.png)

- fromCharCode 가 허용하는 범위는 0부터 65534(0xFFFF) 까지이다. 
	- 모든 유니코드를 커버할 수 없음
	- 높은 코드 포인트 문자는 **써로게이트 값 두 개** 를 합쳐서 표현한다. 
			- `String.fromCodePoint` (ES2015 표준) 

```
유니코드에서는 보통 16비트 코드 단위를 사용해서 문자를 표현하지만, 어느 시점을 넘어서는 문자를 표현하려면 16비트 코드 단위 두 개를 결합해야 한다. 이런 두 개의 코드 단위를 써로게이트 쌍 이라고 부른다. 예시 : 이모지, 고대 문자 
```

**결론**
1. 문자열을 아스키코드로 변환할 때는 `'문자열'.charCodeAt(인덱스, 비어놔도 OK)` 
2. 아스키코드를 문자열로 변환할 때는 `String.fromCharCode(아스키코드, 여러 개 와도 OK)`
3.  → 아스키코드 = charCode 


# 27866. 문자와 문자열 

**문제**
```
단어 S 와 정수 i 가 주어졌을 때, S 의 i번째 글자를 출력하는 프로그램을 작성하시오
```

**풀이**
``` jsx
//charAt, subString, split 메서드를 이용할 수 있음
// 16분

const input = require('fs').readFileSync('./input.txt').toString().split('\n');

const word = input[0]; // 글자
const num  = Number(input[1]);
const answer = word.charAt(num-1);
console.log(answer) ;
```


**🐕 문자열에서 일부(문자, 또는 문자들) 를 추출하는 메서드 : substring, split, charAt** 

``` js 
let str = 'apple';

str.substring(2,3); // apple 에서 index 2에 있는 문자 (p)
str.split('')[2]; // 문자열을 한 글자씩 나뉜 배열로 만든 후, index 2 에 있는 문자
str.charAt(2); // apple 에서 index 에 있는 문자 (p)
```

1. **substring(startIndex, endIndex) 메서드**
	- 문자열에서 **지정된 숫자 인덱스부터 지정된 종료 인덱스 이전까지** 문자열을 반환함
	- endIndex 는 선택 사항, 지정하지 않으면 문자열의 끝까지 추출함 
	- 그래서 `str.substring(2,3)` 는 `index 2` 문자인 `p` 만 추출함

2. **str.split(‘‘) 으로 배열을 만든 후, 인덱스를 지정해서 추출하기**
	- 문자열을 한 글자씩 나누어 배열로 만듬
	- 각 인덱스는 항상 한 글자를 가리킴 

3. **`str.charAt(index)`** 
	- str (문자열) 에서 `index` 에 해당하는 문자를 `char 타입` 으로 반환함 
	- 한 글자씩 반환하며, 배열을 생성하지 않으므로 내부적인 처리 속도가 빠름


**결론**
1. 문자열에서 일부 (문자 또는 문자들) 를 추출하는 메서드는 3가지가 있다 (우선)
2. **문자열에서 문자 단 하나를 추출**하는 건 `charAt(index)`와 `split(‘‘)[index]` 
3. **문자열에서 문자들을 추출**할 수 있는 건 `substring(startIndex, endIndex)`


# 10430. 나머지

**백준**
``` js
let _=require('fs').readFileSync('dev/stdin').toString().trim().split(' ');
let [A,B,C]=_.map(v=>+v);
console.log(`${(A+B)%C}\n${((A%C)+(B%C))%C}\n${(A*B)%C}\n${((A%C)*(B%C))%C}`);
```

**입력**
- 변수( _ ) 에 배열 [ ‘5’, ‘8’, ‘4’] 이  할당된다 (입력이 5 8 4)

### `let [A, B, C] = _.map( .. )`

-  `_.map( .. )` 
	- _ (변수) + `.map( )`
	- `.map()` : 배열의 각 요소에 대해 함수 `v => +v` 를 적용해 새 배열을 만듬

- `v => +v`
	- 여기서 `v` 는 배열의 각 요소를 나타냄 
	- + : 문자열을 숫자로 변환함 !! 
		- 배열의 요소들이 문자열 → 숫자로 변환됨 

- 배열 디스트럭처링 : 배열의 요소들을 개별 변수에 한 번에 할당하는 문법 
	- `[A, B, C]` 에 `_.map(v=>+v)` 이 만든 배열  [‘5’, ‘8’, ‘4’] 을 각각 할당함 


**단항 더하기 (+)**
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Unary_plus
- 단항 더하기 연산자(+) 는 피 연산자 앞 위치하며 피연산자를 평가하지만, 
	**만약 피연산자가 숫자가 아니라면 숫자로 변환을 시도한다** 
	
**map 메서드**
- 배열의 메서드
- 배열의 각 요소에 대해 **주어진 함수를 적용해** 새로운 배열을 생성한다 


**출력** 
- 템플릿 리터럴을 사용해 한 줄로 출력 내용을 생성한 후, 각 결과를 개행 문자(\n) 로 나누어 출력함 → 각 결과를 따로 `console.log` 로 따로따로 출력하는 것 보다 간편함 
- 앞으로는 템플릿 리터럴과 \n 을 사용해서 여러 줄을 출력하자 

**결론**
1. `map()`는 배열의 각 요소에 대해 함수를 적용해 새로운 배열을 만듬
2. 배열 디스트럭처링을 이용해 배열의 요소들을 개별 변수에 한번에 할당할 수 있음
3. `v => +v` 에서 v가 문자일 경우, + 덕분에 숫자로 변환됨
4. 템플릿 리터럴과 개행문자를 사용하면 console.log() 을 한번만 써서 출력 가능함

# 2884.  알람 시계

문제는 맞았지만, 다른 분들 코드를 보다가 감탄한 숏코딩 몇 개가 있어서 정리하려 왔당

``` js
let input=require('fs').readFileSync('dev/stdin').toString().trim().split` `
let H=+input[0]
let M=+input[1]
console.log(M>44?H:H>0?H-1:23,M+(M>44?-45:15))
```

#### <input 을 H 와 M 에 할당하는 방식>

**me** 
``` js
let [H, M] = input.map((v) => +v); // H, M : 10, 10
```

input(배열)의 각 요소에 함수 `v => +v` 를 적용한 새로운 배열을 만듬 
이를 Array destructuring (배열 디스트럭처링) 을 이용해 개별 변수 H, M 에 할당함 

**else** 
``` js
let H=+input[0]
let M=+input[1]
```

input(배열) 의 첫번째, 두번째 요소를 각각 `+` 연산자를 사용해 숫자로 변환, H 와 M 변수에 할당함

**비교**
- me : `map` 함수, 배열 디스트럭처링을 이용해 입력값을 숫자로 변환 (배열 이용)
	- 함수형 프로그래밍 스타일, 확장성과 가독성이 좋음 
- else : 작은 스크립트, 간단한 상황에서 좋음 


#### <삼항연산자 vs if-else 조건문> 

**me**
```
if (M < 45) {
  if (H == 0) {
    H = 23;
    M = M + 60 - 45;
  } else {
    H = H - 1;
    M = M + 60 - 45;
  }
} else {
  M = M - 45;
}

console.log(`${H} ${M}`);```

**else
```

**else**
```
console.log(M > 44 ? H : H > 0 ? H - 1 : 23, M + (M > 44 ? -45 : 15));
```


**이참에 정리하는 삼항연산자**
``` js 
condition ? exprIfTrue : exprIfFalse;
```

- condition : 조건문
- exprIfTrue : Truthy (참) 일 때 실행
- exprIfFalse : Falsy (거짓) 일 때 실행 

- 조건 연산자 라고도 부른다. 
- if … else 문의 대체재로 빈번히 사용된다. 

**Falsy ?** 
```
null, NaN, 0, 비어있는 문자열(""), undefined
```


# 2525. 오븐 시계

``` js
let [hour, minute] = input[0].split(" ").map((v) => +v); // 14, 30
```

-  `input[0]` : 문자열
- `.split(" ")` : 배열로 만듬 (문자 14, 30 요소를 갖는 배열)
- `.map((v) => +v)` : 배열.map 으로 안 요소들을 숫자로 만듬 


#### **몫 만을 구하기**
``` js
hour += Math.floor((minute + need) / 60);
```

- 자바스크립트에서 몫 만을 구하고 싶을 때는 나머지를 제거해주는 내림함수 `Math.floor` 쓰기 
- 우리가 흔히 알고 있는 나누기 ( / ) 는 나눌 때만 사용함
  ``` js
  const num = 10 /3 ;
  console.log (num) // 3.3333 ... 
	```


# 2480. 주사위 세개🌟

#### Math.max()
- 매개변수로 주어진 숫자 중 가장 큰 수를 반환함 

코드를 더 단순하게 줄일 수 있음 ?! 

**나**
``` js 
let input = require("fs").readFileSync("./input.txt").toString().trim().split(" ");

let [d1, d2, d3] = input.map((v) => +v); // 3 3 6

let answer = 0;

  

if (d1 == d2 && d2 == d3) {

  answer = 10000 + d1 * 1000;

} else if (d1 != d2 && d2 != d3 && d1 != d3) {

  answer = Math.max(d1, d2, d3) * 100;

} else {

  // 같은 눈이 2개만 나오는 경우

  if (d1 == d2 && d2 != d3) {

    answer = 1000 + d1 * 100;

  } else if (d1 == d3 && d1 != d2) {

    answer = 1000 + d1 * 100;

  } else if (d2 == d3 && d1 != d2) {

    answer = 1000 + d2 * 100;

  }

}

  

console.log(answer);
```

**GPT** 
``` js
let input = require("fs").readFileSync("./input.txt").toString().trim().split(" ");
let [d1, d2, d3] = input.map(Number); // 3 3 6

let answer = 0;

if (d1 === d2 && d2 === d3) {
  // 세 숫자가 모두 같은 경우
  answer = 10000 + d1 * 1000;
} else if (d1 === d2 || d1 === d3 || d2 === d3) {
  // 두 숫자가 같은 경우
  let same = d1 === d2 ? d1 : d3; // 같은 값을 찾음
  answer = 1000 + same * 100;
} else {
  // 세 숫자가 모두 다른 경우
  answer = Math.max(d1, d2, d3) * 100;
}

console.log(answer);

```


# 25304. 

**문자열을 배열로 만들기** 

``` js
let array = input[i].split(" ");
```

- `input[i]` 는 20000 5 같은 형태의 문자열 
- `.split(" ")` → [20000 5] 형태의 배열로 `array` 에 저장


#### 문자열.`split(" ")`
문자열을 배열로 만들려면 : 문자열.`split(" ")` 
- 공백을 기준으로 요소를 나누어서 배열로 저장함 

# 31403. A+B-C 

기존에는 항상 다음처럼 입력을 받았다. 
(입력이 여러 줄이 아닐 때는 물론 split 을 빼고)
``` js
let _ = require('fs').readFileSync('./input.txt`).toString().trim().split('\n')
```

input.txt
```
3
4
5
```

 3(문자) + 4(문자) 를 해서 34(문자) 를 만든 후 숫자로 변환, 
 5(문자) 를 숫자로 변환해서 34(숫자)-5(숫자) = 29를 구해야 했다.

#### 문제 상황

``` js 
console.log(_[0]+_[1]) // 의도 : 34 , 실제 출력 : 4 
```

#### **문제원인**

캐리지 리턴(\r) 때문이였다. 
텍스트 파일이 Window 에서 작성된 경우, **각 줄 끝에 `\r\n` 문자가 항상 붙는다.**
`split(\n)` 으로 줄바꿈을 기준으로 문자열을 나누어 배열로 만들면서 줄바꿈 문자는 자동으로 제거되지만, `\r` (캐리지리턴) 문자는 각 줄 끝에 남아 있게 된다.

- `trim()` 의 한계 
  ```
    
    3
    4
    5
    
	```
	- 파일의 시작, 끝에 있는 공백 문자 (공백, 줄바꿈 문자) 를 제거함 
	- But 줄 중간에 남아있는 `\r` 는 제거하지 못함 
	  (예 : 3 뒤에 있는 `\r` : `3\r`)
	- 위 경우 `trim()` 는 **시작과 끝의 빈줄을 제거**함

따라서 문자열을 연결할 때 남아있던 캐리지 리턴 문자 때문에
`"3\r" + "4\r"`의 결과가 `"3\r4\r"`이 된 것이다. 

#### 해결한 방법

줄바꿈을 기준으로 줄을 나눈 후, 각 줄에 대해 `trim()` 을 적용해 남아있던 `\r` 캐리지 리턴 문자를 제거하기

``` js
let input = require("fs").readFileSync("./input.txt").toString().trim().split("\n").map(line => line.trim());
```

#### 이전까지 문제가 없었던 이유 ?

이전에는 값들을 처음부터 숫자로 변환해야 풀 수 있는 문제들이였다.
숫자로 변환할 때는 자동으로 캐리지 리턴 문자가 제거된다고 한다. 그래서 이전까지는 문제가 발생하지 않았던 것으로 생각된다.

윈도우 환경에선느 텍스트 파일이 `\r\n` 으로 줄바꿈을 표현한다고 한다. 이는 다른 운영체제에서 동일한 텍스트 파일을 다룰 때 호환성 문제를 피하기 위해 필요하다고 한다. 

#### 결론
1. 텍스트 파일이 Window 에서 작성된 경우, **각 줄 끝에 `\r\n` 문자가 항상 붙는다.**
2. `\r` (캐리지리턴) 문자는 윈도우 환경에서 줄바꿈의 일부분으로 사용된다
3. 숫자로 변환해도 제거되고, 처음부터 입력을 받을 때 `.map(line => line.trim());` 로 수동으로 제거해줄 수 있다. 
