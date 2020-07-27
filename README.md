### 특정 문자열 찾기
```javascript
// 예시 배열
let arr = ['The','fat','cat','sat','on','the','mat.']
// 예시 문장
let str = "The car parked in the garage.";

// 정규식
let reg = /the/g;
// 배열에서 찾기
let item = arr.filter(item => reg.test(item)); 
// 문자열 내부에서 찾기
let item2 = str.split(" ").filter(item => reg.test(item)); 

console.log('item', item);
console.log('item2', item2);
```

### 특정 문자열 찾아 바꾸기
```javascript
// 예시 배열
let arr = ['The','fat','cat','sat','on','the','mat.']
// 예시 문장
let str = "The car parked in the garage.";
// 정규식
let reg = /the/g;

let item = arr.map(item => reg.test(item) ? item.toUpperCase() : item);

let strItem = str.split(" ").map(word => reg.test(word) ? word.toUpperCase() : word);

console.log('arr', item) // ["The", "fat", "cat", "sat", "on", "THE", "mat."]

console.log('str', strItem.join(" ")) // "The car parked in THE garage."
```

### 모든 문장 앞에 첫 글자 대문자 치환하기
```javascript

let str = "i'm a boy. Hello my name is sangheon. i'm 26 years old."

// .으로 문장의 구분 정규식
let reg = /\./;

// 앞에가 대문자인지 확인
let regUpper = /^[A-Z]/;

// 첫문자 추출
let firstLetterReg = /\b[a-z]/;

// 문장 추출한 배열
let sentenceArray = str.split(reg);

// 첫문자가 대문자인경우 그냥 리턴, 아닌경우 첫문자 대문자로 변경
let result = sentenceArray.map(sentence => regUpper.test(sentence) ? sentence : sentence.replace(firstLetterReg, (v) => v.toUpperCase()));

console.log(result.join(". ")); // "I'm a boy Hello my name is sangheon I'm 26 years old."

```