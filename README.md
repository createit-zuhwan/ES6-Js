# ES6-Js / 그외 몰랐던것들

# password 유효성 검사 정규식 

```javascript 
function chkPW(){

 var pw = $("#password").val();
 var num = pw.search(/[0-9]/g);
 var eng = pw.search(/[a-z]/ig);
 var spe = pw.search(/[`~!@@#$%^&*|₩₩₩'₩";:₩/?]/gi);

 if(pw.length < 8 || pw.length > 20){

  alert("8자리 ~ 20자리 이내로 입력해주세요.");
  return false;
 }else if(pw.search(/\s/) != -1){
  alert("비밀번호는 공백 없이 입력해주세요.");
  return false;
 }else if(num < 0 || eng < 0 || spe < 0 ){
  alert("영문,숫자, 특수문자를 혼합하여 입력해주세요.");
  return false;
 }else {
	console.log("통과"); 
    return true;
 }

}


```
# loop async 
loop 안에서 비동기 처리를 하려면

for await 를 사용한다 , 혹은 promise all 을 사용해도 된다

``` typescript
const employeeList = await employeeModels.getCompanyList(where);
for await (let item of employeeList) {
    const employee: any = item.toJSON();
    list.push({
      ...employee,
    });
  }


```
# 단축평가 평가
단축평가란 , 예를들어서 And 연산에 대한 것은 두값을 모두 평가하지 않아도 될때가 있는데 , 예를들어서 xfalse 이고 y 가 true 일때 x && y는 false 를 반환한다. y를 평가할 필요도없이 false 이고 ,
x || y 에서 x 가 참이면 y를 비교할 필요없이 true 이다. 이러한동작을 단축 평가라고한다.

1) **단축평가는 이럴때 사용된다. 
``` javascript
//변수할당할때 
const status = true;
let temp = '';
temp = status && 'test!';
console.log(temp)
```
```javascript
// null / undefined 체크할때사용 
const test = (params) =>{
 // console.log(params);
  const res = params || '비어있음'
  console.log(res)
}

test();


```

# jwt 1
json web token

jwt 는 인증에 필요한 정보들을 암호화시킨 토큰을 의미한다. Access token 을 http 헤더에 실어서 서버로 보낸다, 쿠키 세션방식은 세션 저장소가
필요하기 때문에 메모리 과부하 문제가 생길 수 있지만 , jwt 방식은 서버 리소스를 사용하지않는다.

# jwt 형식
1) header : 정보를 암호화할 방식 , 타입등
2) payload : 서버에서 보낼 데이터 , 일반적으로 유저 고유 id , 유요기간등이 들어간다.(민감한 정보는 넣지않음)
3) Verify Signature : Base64 방식으로 인코딩한 header , payload , secret key를 더해 만든다.
4) 
# 자바스크립트에서 배열은 배열이 아니다.
배열은 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료구조를 말한다.

즉 배열의 요소는 하나의 타입으로 통일 되어 있으며 서로 연속적으로 인접해있는데 이러한 배열을 밀집 배열 이라고한다.

배열의 요소는 동일한 크기를 갖으며 , 빈틈없이 연속적으로 이어져 있으므로 인덱스를 통해 단 한번의 연산으로 임의의 요소에 접근 , 시간복잡도 O(1)할수 있다. 이는 매우 효율적이며 , 고속으로 동작하는데.

자바스크립트의 배열은 위와같은 배열의 의미와 조금 다르다. 자바스크립트의 배열은 일반적인 배열의 동작을 흉내낸 특수한 객체이다.

자바스크립트 배열은 인덱스를 프로퍼티 키로 갖고 있고 , length 프로퍼티를 갖는 '특수한' 객체이다. 자바스크립트 배열의 요소는 사실 프로퍼티 값이다.

# 문자열 공백제거하는방법
```javascript

let str1 = '             how are you      to  day        everyone';
console.log(str1.trim())// 앞뒤공백제거
console.log(str1.replace(/\s+/g, ''))
console.log(str1.split(' ').filter(el=>el !='').join(' '))
console.log(str1.replace(/\s+/g, ' '))


```
# 배열에서 중복제거하기 / + Array.from 으로 배열생성 
1) set
2) filter + indexOf()
```javascript
const temp = [1,2,3,4,4,4,4,4,5]
let s = new Set(temp)
s = Array.from(s)
console.log(s)
```
# Hoisting
함수 안에 있는 선언들을 모두 끌어 올려서 해당 함수 유효범위의 최상단에 선언하는것을 말한다.
# 객체의 병합(복사)
```javascript
//객체의 복사는 이렇게하면된다.
let objSource = {item1:'test1',item2:'test2'}
// 빈객체와 원본객체를 병합 
let objClone = Object.assign({},objSource)
console.log(objClone)
// 병합원칙
//1) 없는 속성은 추가한다.
//2) 중복되는 속성은 원본객체(두번째 파라미터) 의 속성값으로 덮어쓴다.

```
# 객체의 상속
```javascript
const originalObj = {name:'hello',age:5,};
const childObj = Object.create(originalObj);
//console.log(childObj.name)
// 부모 객체값 변경 
originalObj.name = '변경햇음';
console.log(childObj.name)

```
# 호이스팅 대상

1) var 변수 선언 , 함수선언문
2) let / const 변수 선언과 함수표현식에서는호이스팅이 발생하지 않는다.
``` javascript
foo();
foo2();
function foo() { console.log('hh') }
foo2 = function() { console.log('hh2')} // 이거 안댐

```
# 호이스팅 우선순위

변수 선언이 함수 선언보다 위로 끌려옴.

# 래퍼 객체
래퍼객체란 원시데이터 타입(string,number...등)을 감싸는 객체이다.

다음예시를 보자

```javascript
let str = 'fkmfke';
console.log(str.length)
```
str 은 원시데이터 타입 string 을담은 변수이다. 

그런데 str.length 에서 . 은 객체의 프로퍼티에 접근할때, 객체에 접근할때 사용하는것인데. 이것은 무엇일까?

자바스크립트는 원시형 데이터 타입도 내부적으로는 객체로 래핑해서 구현한다. 즉 , 원시형 변수를 선언했지만 , 내부적으로는 객체가 생성되는것이다.

# 자바스크립트에서 함수는 일급객체이다.
일급객체란 변수나 데이터에 할당할수 있어야하는것

객체의 인자로 넘길수 있어야한다

객체의 리턴값으로 리턴 할수 있어야하는것 

# Math.abs() , Math.sign()
Math.abs() => 숫자의 부호 없는 양의 숫자 값을 반환한다.
Math.sign() => 숫자의 부호를 알려준다, 양수이면 1 , 0이면 0 , 음수이면 -1 을 반환, 숫자가 아닌경우 NaN반환
# Array.prototype.filter()
filter() 를 사용하면 , 파라미터로 넘긴 함수의 조건을 만족하는 요소만을 모아 배열로 반환한다. 즉 , 필터링을 해주고 필터링한 요소를 여러개를 반환할때 사용한다. 

``` javascript

const arr1 = [{name:'hello',age:20},{name:'테스트',age:21},{name:'테스트2',age:19},{name:'테스트3',age:19},{name:'테스트4',age:19},]

const filtering = arr1.filter((item)=> item.age === 19);
const filtering2 = arr1.filter((item)=> item.age > 19);
//console.log(filtering)
console.log(filtering2)


```
``` javascript
// 사용 예시2 0,null , nan , 'undefined'를 제외하고 필터링하기 
var arr = [
  { id: 15 },
  { id: -1 },
  { id: 0 },
  { id: 3 },
  { id: 12.2 },
  { },
  { id: null },
  { id: NaN },
  { id: 'undefined' }
];


const result = arr.filter((v,i)=>{
  if(v.id && v.id !== 'undefined'){
    return arr
  }
})
console.log(result)




```
# Array.prototype.sort()
배열을 정렬한다.

```javascript
/**
 * Array.prototype.sort()
 * arr.sort([compareFunction])
 */

/**
 * compareFunction
 * 정렬순서를 정의하는 함수 
 * 이 값이 생략되면 배열의 element들은 문자열로 취급되서 유니코드 값 순서대로 정렬된다.
 */
// compareFunction 함수의 형식 
function compare(a, b) {
  if (a is less than b by some ordering criterion) {
    return -1;
  }
  if (a is greater than b by the ordering criterion) {
    return 1;
  }
  // a must be equal to b
  return 0;
}
/**
 * compareFunction(a,b) 가 0 보다 작은경우 a를 b보다 낮은색인으로 정렬한다. a가 먼저온다
 * compareFunction(a,b) 가 0을 반환하면 a,b를 서로 변경하지않고 모든 다른요소에 대해 정렬한다.
 * compareFunction(a,b) 가 0보다 큰경우 b를a 보다 낮은 인덱스로 정렬한다.
 */
arr3.sort((a,b)=>{
  console.log(a,b)
  if(a > b) return 1;
  if(a === b) return 0;
  if(a < b) return -1;
});

//console.log(arr3) // 정렬됨 (숫자 낮은거 기준으로)
//console.log(arr3.reverse()) // 반대로 정렬됨

const items = [
  { name: 'Edward', value: 21 },
  { name: 'Sharpe', value: 37 },
  { name: 'And', value: 45 },
  { name: 'The', value: -12 },
  { name: 'Magnetic', value: 13 },
  { name: 'Zeros', value: 37 }
];
/**
 * 객체 정렬하기, value 를 기준으로 
 */
items.sort((a,b)=>{
  if(a.value > b.value) return 1;
  if(a.value === b.value) return 0;
  if(a.value < b.value) return -1;

})

/**
 * 객체 정렬하기, value 를 기준으로 
 */
items.sort((a,b)=>{
  if(a.name > b.name) return 1;
  if(a.name === b.name) return 0;
  if(a.name < b.name) return -1;

})
//console.log(items) // value 가 낮은것부터 정렬
//console.log(items.reverse()) // value 가 높은것부터 정렬
//console.log(items) // name 에서 알파벳 순서대로 정렬
console.log(items) // name 에서 알파벳 순서 반대로 정렬




```

# 문자열로 들어온 숫자 내림차순으로 정렬하는법 

``` javascript
const solution = (n) => {
    let answer = 0;
    let temp ='' 
    temp = n.toString() // 들어온 parameter 를 string 
    temp = temp.split('').sort().reverse().join('') // split 한다음 문자열을 배열로 생성 , reverse 후 , join 
    return parseInt(temp);
}


```

# 문자열 정렬하는 방법 ( reverse )  오름차순 

 ```javascript

const arrSort = s => {
   let a = s.split('').sort().reverse().reduce((a,b) => a+b) 
   console.log(a) 
   }
    arrSort("ceasgwZ")




```
1. 들어온 문자열을 쪼개어 배열로 만든다.(split)

2. 오름차순으로 정렬한다.(sort)

3. 반전시킨다(reverse)

4. 문자 하나하나 들어가있는 배열을 합친다.(reduce)

``` javascript
// 전체 문자열 반대로 뒤집기 
var name = "test";

var nameReverse = name.split("").reverse().join(""); 





```

```javascript
// 자연수 뒤집어 배열로 만들기
// n => 12345 를 뒤집어서 [5,4,3,2,1] 로 만들고자 할때.
function solution(n) {
    let answer = [];
    let str = parseInt(n) + ''
    let a = str.split('').reverse()
    a.forEach((i)=>answer.push(parseInt(i)))
    return answer;
}


```

# parseInt() 
문자열 인자를 파싱하여 특정 진수 의 정수를 반환한다.
```javascript
parseInt(string)
parseInt(string, radix)
/**
*
*string의 진수를 나타내는 2부터 36까지의 정수입니다. 주의하세요. 기본 값이 10이 아닙니다! Number 자료형이 아닌 경우 Number로 변환합니다.
*
**/

```

# 배열에서 배열 element 요소를 정수로 바꾸기 

```javascript

// n => parameter 123
const solution = (n) => {
    let answer = 0;
    let temp = n.toString(); //123을 to String
    temp = temp.split(""); // "123" 을 배열로 만든다 ["1","2","3"]
    // map 을 이용하여 순회하여 각 요소들을 정수로 casting 해준다.
    temp = temp.map((x)=>{
        return parseInt(x)
    })
    console.log(temp);
  return answer;
}


```
# 문자열에서 띄어쓰기하기 (문자열에 공백을 추가하기 (만약) )

예를들어 두개 문자 hello,world 가 있는데 이 두개 사이에 공백을 추가해서 hello world 로 하고싶다면
 ```javascript
let str1 = '문자열1';
let str2 = '문자열2';
let last = ','
str1 = str1.concat(last).concat(str2).split(',').join(' ');

console.log(str1)
 
  ```
  
# Math.min / Math.max 배열에서 사용하기

```javascript

const test = [1,2,3,4,5,6]
let temp = Math.max(...test); // test 배열에서 최대값을 가지는 element 를 반환한다.
let temp = Math.min(...test); // test 배열에서 최소값을 가지는 element 를 반환한다.


// 배열에서 최소값을 찾고 , 최소값 삭제 
function solution(arr) {
    let answer = [];
    let index = '';
    let min = Math.min(...arr);
    index = arr.indexOf(min); // 삭제할 최소값 item 의 index  
    arr.splice(index,1)
    // 최소값이 없는경우 return -1 
    if(arr.length === 0){
        arr.push(-1)
        return arr
    }
    return arr;
}



```
# 배열에서 최소값 을 찾고 , 최소값을 삭제하기

```javascript

// 배열에서 최소값을 찾고 , 최소값 삭제 
function solution(arr) {
    let answer = [];
    let index = '';
    let min = Math.min(...arr.map(item => {
        return item
    }));
    index = arr.indexOf(min); // 삭제할 최소값 item 의 index 
    arr.splice(index,1)
    console.log(arr)
    if(arr.length === 0){
        arr.push(-1)
        return arr
    }
    return arr;
}


```
# padStart
``` javascript
//padstart로 휴대폰번호 마스킹하기

 const solution = (phone_number) => {
    // String.prototype.padStart() 사용
    const last4Digits = phone_number.slice(-4);
    const maskedNumber = last4Digits.padStart(phone_number.length, '*');
  
    return maskedNumber;
}



```
# Json 값만 배열로 추출하기

``` javascript

const arr1 = {value1 : 13 ,value2 : 12 , value3 : 14 , value4 : 15}
let temp = Object.values(arr1);


console.log(temp)


```
# shift , unshift

배열의 맨앞에 요소를 추가할때는 unshift , 삭제는 shift 할때 사용한다.

stack 구조 (Last in first out) 으로 동작하기 때문에 stack 을 구현할 경우 , shift , unshift를 사용하도록 한다

```javascript

const arr = [];
arr.unshift('a');
arr.unshift('b');
arr.unshift('c');


```
# find 

find() 를 사용하여 배열을 순환하다 , 파라미터로 넘긴 함수의 조건을 만족하는 요소가 발견되면 조건에 해당하는 요소를 반환하고 즉시 종료한다.
이때 반환값은 하나를 반환한다 즉, find()를 통해 , 조건을 찾게되면 순환문이 멈추고 , 조건을 (하나) 리턴하고 종료한다.
``` javascript
const arr1 = [{name:'hello',age:20},{name:'테스트',age:21},{name:'테스트2',age:22},{name:'테스트3',age:24},{name:'테스트4',age:19},]

const found = arr1.find((item)=> item.age === 19);
console.log(found)


```
find() 의 사용예시는 다음과 같다.

```javascript
// programmers 1단계 문제 서울에서 김서방 찾기 에서.

const solution = (seoul) => {
    let answer = '';
    const found = seoul.findIndex(element => element === 'Kim');
    //console.log(found)
    answer = `김서방은 ${found}에 있다`
    console.log(answer)
    return answer;
}


```


# some (조건을 만족하는 요소가 있는지 확인하기 )
조건을 만족하는 요소가 1개라도 있으면 true 그렇지 않으면 false 를 반환 , 조건을 만족하는 요소가 있으면 남은 요소들을 더 확인하지 않고 true 를 반환하고 종료한다.
``` javascript
const arr1 = [{name:'hello',age:20},{name:'테스트',age:21},{name:'테스트2',age:19},{name:'테스트3',age:19},{name:'테스트4',age:19},]

bool_check = arr1.some(item => item.name === '테스트4')
console.log(bool_check)

```
# reduce 

``` javascript 
// reduce 사용시 , 배열의 합구하기 
const arr1 = [1,2,3,4,5];
const sum = arr1.reduce((stack,item)=>{
  return stack+item
},0)
console.log(sum)
// foreach 사용시 배열의 합구하기 
let globalVar = 0;
arr1.forEach((item,index)=>{
  globalVar = globalVar+item
})
console.log(globalVar)



```
# reduce 를 이용하여 배열의 평균 구하기


``` javascript
const arr = [1,2,3,4]

let res = arr.reduce((accumulator,currentValue,currentIndex,array)=>{
return (accumulator + currentValue)
})


console.log(res/arr.length)


```
# reduce 이용하여 단일 배열로 단순화 하기

```javascript
const arr2 = [1,[2,3],4,[5,6,7]];
// reduce 중첩배열 단순화 
const arr_concat = arr2.reduce((stack,item)=>{
  return stack.concat(item);
},[]);

console.log(arr_concat)
// reduce 를 이용한 중첩배열 단순화 + join 
const arr3 = [1,[2,3],4,[5,6,[7,8,9]]];
const arr_concat2 = arr3.reduce((stack,item)=>{
  return stack.concat(item);
},[]);
console.log(arr_concat2.join(',').split(','))

```
# concat(배열 합치기)

```javascript
const arr3 = ['hello','world','test']
const arr4 = ['test2','test3','test4']
// foreach 
arr3.forEach((item,index)=>{arr4.push(item)});
console.log(arr4)
// concat 
arr5 = arr3.concat(arr4)
console.log(arr5)

```
   
# splice

```javascript

const str1 = [1,2,3,4,5];
// splice 삭제 
//str1.splice(0,2);
//console.log(str1)
// splice(시작인덱스 , 삭제할 요소 길이 , 추가 요소1 , 추가 2...)
// splice => 배열 요소들 사이에 요소를 추가할수있다.
// 단 , 요소 사이에 추가하기 위해서 기존 에있는 요소를 삭제한뒤 추가해야함
str1.splice(1,1,20);
str1.splice(3,1,50)
console.log(str1)


// splice 요소추가
const str3 = ['펭수','라이언','어피치','콘','브라운'];

// => [네오 , 튜브 , 프로도 , 브라운 ]
str3.splice(0,4,'네오','튜브','프로도')
console.log(str3)

```
# 문자열에서 중복된 값 제거하기 

``` javascript
function removeDuplicateCharacters(string) {
  return string
    .split('')
    .filter(function(item, pos, self) {
      return self.indexOf(item) == pos;
    })
    .join('');
}
```
# javscript 에서 function 

자바스크립트에서 function 은 일급객체라고 부른다. 일급객체의 특징은 다음과 같이 설명한다.

첫째. 일급객체는 변수나 데이터 구조 안에 담을수있다.
둘째. 인자로 전달할 수 있다 (callback)

셋째. 반환 값 (return value 로 사용할수 있다)

넷째. 런타임에 생성할 수 있다.

다섯. 할당에 사용된 이름과 관계 없이 고유하게 식별할 수 있다.

# Closure (클로저)

클로저란 내부에 선언된 함수가 외부함수의 지역변수를 사용할수있는 (접근할수있는것) 을 말한다.

클로저를 이용하여 전역변수를 줄일수 있고 , 비슷한형태의 코드를 , 재사용률을 높일 수 있다.

``` javascript

// 내부 함수가 외부함수의 지역변수에 접근할수있다.
function outerFnc(){
  let outerVar = 'outerVar';
  return function innerFnc(){
    console.log(outerVar);
    //return outerVar;
  }
}

let inner = outerFnc();
inner()
//console.log(inner())


```

화살표함수로 이렇게 바꿀수 있다.

``` javascript



const outerFnc = () => {
  let outerVar = 'outerVar';
  return innerFnc = () =>{
    console.log(outerVar);
  }
}

let inner = outerFnc();
inner();


```

# closure 의 응용

버튼을 클릭하면 count 가 증가하는 function 이 있다고 가정하고 , 이를 closure 를 이용하여 구현 해본다.

```javascript

// 전역변수를 사용한 예시 
let globalVar = 0;

 function handleCilck () {
  globalVar ++;
  console.log('globalVar =>', globalVar)
  return globalVar;
}




```

```javascript

// closure 를 사용 
const btn = document.querySelector('button')

let handleCilck = (callback) => {
  let count = 0
  return ()=>{
    count++
    return callback(count)
  }
}

btn.addEventListener('click',handleCilck((result1)=>{
  console.log(result1);
}))

```


# this 

this 가 가르키는 바는 일반적인 context 에서는 window 객체 ( global ) 을 가리킨다. 하지만 이 상황에서는 이야기가 달라진다. 
``` javascript 

let obj = {
  myVar: 'foo',
  
  myFunc: function() { 
    let self = this;
    console.log(this.myVar)   
 
    setTimeout(()=> {
      console.log(this.myVar)
    }, 1000)
  }
}
obj.myFunc() 


```
obj(객체안)에서 this 는 obj 를 가리키므로 , this.myVar 는 obj.myVar 를 가리킨다.

# Arrow functions 

화살표함수는 다음과 같은 표현식에서 대체할수있다. 단 arrow function 은 , context 에 따라 this 가 달라진다.

```javascript
//기존 function 선언방식 
function tempFnc(){

}
```

```javascript 
//arrow function 선언방식
()=>{

}
const myFnc = () => {

}

```

마찬가지로 콜백함수도 화살표함수로 이렇게 바꿀수 있다.

```javascript

const callFnc = (param1,callback) =>{
    let num2 = 21;
    return callback(param1 + num2);
}

const test = callFnc(2000,(result)=>{
  console.log(result)
})

```




# Template Literals

템플릿 리터럴을 통해 문자열을 연결하기 위해 (+) 연산자를 사용할 필요없이 백틱(`) 을 통해 문자열 내에서 변수를 사용할수있다.

```javascript
let globalVaribale;

const myFnc = () =>{
  this.globalVaribale = 20;
  console.log(`number => ${this.globalVaribale}`)
}
myFnc()

```

# map 
map를 이용하여 여러개의 데이터를 순회할수있다.

``` javascript
const myArrary = [0,1,2,3,4,5];

let arr2 = myArrary.map((item) => {
  console.log(item)
});

```

# Default parameters

``` javascript 
const myFnc = (param1 , param2 = 22) => {
  return param1 + param2;
}

console.log(myFnc('test1'))

```

# 비구조화 할당 
``` javascript
// object 비 구조할당 
const temp1 = {
  key1:'value1',
  key2:'value2',
  key3:'value3',
};

let {key1 , key2 , key3} = temp1;

console.log(key1,key2,key3);
// array 비 구조할당 
const tempArr = [10,20,30];

let [val1,val2,val3] = tempArr
console.log(val1)


```

# 나머지 매개변수 
``` javascript 
const myFnc = (...args) =>{
  let sum = 0;
  const result = args.map((item) => {
  sum+=item
});
  return sum
}

console.log(myFnc(1,2,3))
// ...args 는 parameter들을받아서 배열로 만든다는 의미이다.
```

# Spread Operator 
특정 객체 , 배열값을 다른객체 , 배열로 복제하거나 옮길때 사용한다. 
```javascript
let obj = {
  a:10,
  b:20,
}
let newObj = {...obj};

console.log(newObj)

let arr = [1,2,3]

let newArr = [...arr];

console.log('newArr =>' , newArr)

```
# destructuring 
디스트럭쳐링이란 , 구조화된 배열이나 객체를 비구조화 하여 개별적인 변수에 할당하는 것이다. 

종류에는 두개가 있는데 하나는 배열 디스트럭처링 , 또하나는 객체 디스트럭처링이다. 
# Array destructuring (배열 디스트럭쳐링)

``` javascript
const arr = [1,2,3];

const [o,t,q] = arr;

console.log(o,t,q)

```

# Object destructuring (객체 디스트럭쳐링)

``` javascript
const obj ={
  key1:'1312',
  key2:'4444',
}


const {key1 , key2} = obj;

console.log(key1,key2)


const {p1,p2,p3 = '20'} = { p1 : 'ee',p2 : 'rrqq'};

console.log(p1,p2,p3)

const person = {
  name: 'Lee',
  address: {
    zipCode: '03068',
    city: 'Seoul'
  }
};

const { name , address: { city } } = person;

console.log(name , city);

```
# promise
기존 callback function 을 사용했을때 나타나는 단점을 보완하기 위해 promise 를 사용하여 이를 해결할수있다. 

``` javascript
const temp = () =>{
  return new Promise((resovle, reject) =>{ 
    resovle(20);
  })
}
temp()
.then((res)=>{
  return res + 1
})
.then((res)=>{
  return res + 1
})
.then((res)=>{
  return res + 1
})
.then((res)=>{
  return res + 1
})
.then((res)=>{
  return res + 1
})
.then((res)=>{
  console.log(res);
})

```
이렇게 비동기 작업을 한뒤 , then function 에서 그 후의 작업을 할수있다. , .then 을 이어나가서 진행하는 방식을 promise chainning 이라고 한다. 

# async await 
promise channing 코드를 간결하게,보완하기 위해서 사용한다.
``` javascript 

const asyncF = () =>{
  return new Promise((resolve, reject)=>{
    resolve(20);
  })
}


const tt = async() =>{
  let num = 0;
  let t = await asyncF();
  let t2 = t+40;
  console.log(t2)
} 
tt();

```

# class 
``` javascript 

class A {
  constructor(param1,param2){
    this.param1 = param1;
    this.param2 = param2;

  }
  methods(){
    console.log('methods');
    console.log(this.param1);
    console.log(this.param2);
    
  }
}

const a1 = new A(20,30);
a1.methods();

```
# String.includes()
해당 문자열이 포함되어있는지 확인 후 true 를 리턴한다.
```javascript 

let text = "Hello world, welcome to the universe.";
text.includes("world")    // Returns true

```

# String.startsWith()
문자열이 어떤것으로 시작되는지 판별한다 
``` javascript 
let text = "Hello world, welcome to the universe.";

text.startsWith("Hello")   // Returns true

```
# JavaScript Array.includes() 

배열 요소중 특정 요소엘레멘트가 있는지 확인하고 true / false 를 return 한다.
``` javascript 
const fruits = ["Banana", "Orange", "Apple", "Mango"];

console.log(fruits.includes("Mango"))


```




