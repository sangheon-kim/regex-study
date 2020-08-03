# Regex Study (made by Sangheon Kim)

### 특정 문자열 찾기

#### created By 2020.07.25

```javascript
// 예시 배열
let arr = ["The", "fat", "cat", "sat", "on", "the", "mat."];
// 예시 문장
let str = "The car parked in the garage.";

// 정규식
let reg = /the/g;
// 배열에서 찾기
let item = arr.filter((item) => reg.test(item));
// 문자열 내부에서 찾기
let item2 = str.split(" ").filter((item) => reg.test(item));

console.log("item", item);
console.log("item2", item2);
```

### 특정 문자열 찾아 바꾸기

#### created By 2020.07.26

```javascript
// 예시 배열
let arr = ["The", "fat", "cat", "sat", "on", "the", "mat."];
// 예시 문장
let str = "The car parked in the garage.";
// 정규식
let reg = /the/g;

let item = arr.map((item) => (reg.test(item) ? item.toUpperCase() : item));

let strItem = str
  .split(" ")
  .map((word) => (reg.test(word) ? word.toUpperCase() : word));

console.log("arr", item); // ["The", "fat", "cat", "sat", "on", "THE", "mat."]

console.log("str", strItem.join(" ")); // "The car parked in THE garage."
```

### 모든 문장 앞에 첫 글자 대문자 치환하기

#### created By 2020.07.27

```javascript
let str = "i'm a boy. Hello my name is sangheon. i'm 26 years old.";

// .으로 문장의 구분 정규식
let reg = /\./;

// 앞에가 대문자인지 확인
let regUpper = /^[A-Z]/;

// 첫문자 추출
let firstLetterReg = /\b[a-z]/;

// 문장 추출한 배열
let sentenceArray = str.split(reg);

// 첫문자가 대문자인경우 그냥 리턴, 아닌경우 첫문자 대문자로 변경
let result = sentenceArray.map((sentence) =>
  regUpper.test(sentence)
    ? sentence
    : sentence.replace(firstLetterReg, (v) => v.toUpperCase())
);

console.log(result.join(". ")); // "I'm a boy Hello my name is sangheon I'm 26 years old."
```

### 핸드폰 번호 확인해서 '-' 붙이기

#### created By 2020.07.28

```javascript
// 양식에 맞는지 확인
const phone = [
  "01022848367",
  "010-1234-5678",
  "0109999999",
  "01056781234",
  "010 1111 2222",
  "022121234",
];

// 핸드폰 번호 정규 표현식
const phoneReg = /^([0-9]{3}).{0,1}([0-9]{4}).{0,1}([0-9]{4})$/;

// 치환해주는 공장
const factory = (num) => num.replace(phoneReg, "$1-$2-$3");
// 핸드폰 형식인것들은 치환해주고 아닌건 그대로 출력
let array = phone.map((item) => factory(item));

console.log(array); //["010-2284-8367", "010-1234-5678", "0109999999", "010-5678-1234", "010-1111-2222", "022121234"]
```

### 생년월일 체크 공식

#### created By 2020.07.29

```javascript
const birth = ["1995-09-06", "19951221", "1234 09 06"];
const birthReg = /^([1|2]{1}[0-9]{3}).{0,1}([0,1]{1}[0-9]{1}).{0,1}([0-3]{1}[0-9]{1})$/;

const factory = (birth) => birth.replace(birthReg, "$1-$2-$3");

let array = birth.map((item) => factory(item));

console.log(array); // ["1995-09-06", "1995-12-21", "1234-09-06"]
```


### 공백제거
#### created By 2020.07.29
```javascript
var fileNames = ['1. abc', '2.       abc', '3.abc' ];

var regex7 = /([0-9].)\s+([a-z,A-Z]{3})/;

let array = fileNames.map(item => item.replace(regex7, '$1$2'))

console.log(array) // ["1.abc", "2.abc", "3.abc"]
```

### @2x 이미지 전부 -2x로 파일명 치환
#### created By 2020.08.03
##### svn에 @는 안올라가서 직접 만듬
```javascript
const fs = require("fs");
// glob 모듈의 경우 외부 모듈이니 설치해주세요 
const glob = require("glob");
// 이미지 파일 경로를 지정해줍니다.  
const imgPath = 'src/assets/img/src/'
 
// 정규표현식에 앞부분 경로를 설정해줍니다.  
 const reg = /((src\/assets\/img\/src\/)(((.+)@2x)(.png)))/
  
 glob(`${imgPath}/*@2x.png`, function (err, files) {
  files.map(item => {
   fs.rename(item, item.replace(reg, '$2$5-2x$6'), (err) => {
   if (err) throw err;
   console.log('Complete By Code that made by Sangheon')
  })
 })
});
```

### 파일명 공백 제거 및 한자리앞에 0 붙이기Layer 1.png -> Layer01.png
#### created By 2020.08.03
##### gif sprite 이미지 처리 후 애니메이션 해야하는데 generator에서 이름 오름차순하는데 1 다음 2가 읽혀야하는데 10이 읽혀져서 그거 막으려고 만듬.
```javascript
const fs = require("fs");
// glob 모듈의 경우 외부 모듈이니 설치해주세요 
const glob = require("glob");
// 이미지 파일 경로를 지정해줍니다.  
const imgPath = 'image/*'
// png아닌거 바꾸고싶으면 확장자 변경해주세요
const reg = /^(.+)\s+(.?\d)+(\.png)$/

glob(`${imgPath}/*.png`, function(err, files) {
  files.map(item => {
    fs.rename(item, item.match(reg)[2].length === 1 ? item.replace(reg, '$10$2$3') : item.replace(reg, '$1$2$3'), (err) => {
      if (err) throw err;

      console.log('Complete By Code that made by Sangheon')
    })
  })
})
```