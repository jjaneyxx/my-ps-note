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

