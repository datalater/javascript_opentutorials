copyright ⓒ JMC 2017

주요 소스: 생활코딩 JavaScript for Web Browser

resume:

---

## 8강 BOM : (3) Location 객체

#### Location 객체의 기능

+ 현재 브라우저 창에 열려 있는 문서의 url을 알려준다.

#### 현재 윈도우의 URL 알아내기

```
> console.log(location.toString(), location.href);
```

현재 웹 페이지 url을 알려준다. `location.toString()`와 `location.href` 둘 다 같은 기능이나 `.href` 를 쓰는 것이 정석이다.

```
> console.log(location);
```
location 객체에 대한 다양한 정보를 보여준다. 다양한 정보란 location 객체의 property를 뜻한다.

#### URL Parsing

+ URL을 의미 단위대로 조각조각 파싱한다.

```
> console.log(location.host);
opentutorials.org
```

현재 웹 페이지의 호스트(`host`)를 보여준다. 호스트란 웹 사이트를 식별하는 주소를 말한다.

```
> console.log(location.pathname);
/module/904/6634
```

`pathname`은 어떤 웹 서버에 접속했을 때 `host`를 제외한 구체적인 정보를 보여준다.

```
> console.log(location.search)
?id=10
```

`serach`는 url에서 물음표부터 시작하는 쿼리 부분을 보여준다.

#### URL 변경하기

+ 사용자를 다른 URL로 이동시키기 (redirect)

```
> location.href = "http://the7mincheol.blog.me";
```

```
> location = "http://the7mincheol.blog.me";
```

현재 웹 페이지가 `http://the7mincheol.blog.me`로 이동한다. 두 코드 모두 기능이 동일하다. 단, `location.href`를 사용하는 것이 더 명시적인 방법이다.

+ 현재 웹 페이지 reload 하기

```
> location.reload();
```




---

## 7강 BOM : (2) 사용자와 커뮤니케이션 하기

#### 사용자와의 커뮤니케이션이란 무엇인가

+ 사용자에게 정보를 제공하거나, 사용자로 하여금 정보를 입력하게 해서 처리한다

#### alert

```
> alert('Hello World');
```

+ 경고창
    + 사용자에게 정보를 제공하거나
    + 사용자에게 오류에 대한 경고를 하거나
    + 개발자가 디버깅의 용도로 무언가를 확인할 때 사용한다.

#### confirm

```
> confirm('ok?');
```

+ 컨펌창
    + 사용자가 긍정적인 피드백을 주느냐, 부정적인 피드백을 주느냐에 따라
    + 개발자가 조건문을 통해 로직의 흐름을 분기시킬 수 있는 기능을 제공한다.

```
<body>
    <input type="button" value="confirm" onclick="func_confirm()" />
    <script>
        function func_confirm(){
            if(confirm('ok?')){
                alert('ok');
            } else {
                alert('cancel');
            }
        }
    </script>
</body>
```

#### prompt

```
> prompt('id?');
```

+ 프롬프트
    + 사용자로부터 입력을 받는 기능을 제공한다.
    + 사용자가 입력한 값을 받아 JavaScript가 동작할 수 있는 기능을 제공한다.

```
<body>
    <input type="button" value="confirm" onclick="func_prompt()" />
    <script>
        function func_prompt(){
            if(prompt('id?') == 'jay'){
                alert('welcome');
            } else {
                alert('fail');
            }
        }
    </script>
</body>
```

---

## 6강 BOM: (1) 전역객체 window

#### alert() == window.alert()

+ DOM, BOM 그리고 사용자가 만드는 모든 변수나 함수는 전역객체 window에 소속된다.
+ 즉, DOM, BOM, 사용자 변수, 사용자 함수 모두 window의 property이다.
+ 따라서 `alert(Hello World)`는 `window.alert(Hello World)`와 동일하다.
+ `alert()`함수 또한 window에 이미 포함되어 있기 때문이다.

---

## 5강 Object Model 개념 : window, DOM, BOM, JavaScript Core

#### 질문

+ JavaScript로 브라우저를 제어한다는 것이 어떤 의미일까?

#### 웹 브라우저를 구성하는 Object Model 체계 도식화

![브라우저 객체 구성](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/904/2229.png)

#### window

+ 전역 객체
+ DOM, BOM, JavaScript Core를 포함하는 최상위 객체이다.
+ 즉, DOM, BOM, JavaScript Core는 window의 property이다.


#### DOM (Document Object Model, document)

+ 웹 페이지의 문서를 제어한다.
    + ex. `<body>`, `<img>` 같은 태그를 제어할 수 있다.

#### BOM (Browser Object Model)

+ 웹 브라우저를 제어한다.
    + ex. 현재 웹 브라우저가 가리키고 있는 url을 알아낼 수 있다.
    + ex. 현재 웹 브라우저가 표시하고 있는 웹 페이지를 reload 할 수 있다.
    + ex. 현재 웹 브라우저에 경고창을 띄울 수 있다.

#### JavaScript Core

+ 브라우저를 제어한다.
+ Google Apps Script를 제어한다.
+ node.js를 제어한다. (server측 javascript)

```
JavaScript Core에 대한 설명이다. 어려우니 한 번 듣고 넘어가라.

우선 JavaScript로 브라우저 내 객체인 BOM과 DOM을 제어할 수 있다.
그러나 인터넷 호스트 환경에는 브라우저만 존재하는 것이 아니다.
다양한 호스트 환경이 존재한다.
그 사례 중 대표적인 것이 Google Apps Script와 node.js이다.

Google Apps Script (GAS) 환경에서는 BOM과 DOM이 존재하지 않는다.
가령, Google Spreadsheet, Gmail에서는 그 시스템 고유의 객체가 존재한다.
그러므로 GAS 객체를 제어하려면 JavaScript로 제어해야 한다.

node.js도 마찬가지로 브라우저와는 다른 객체들을 가지고 있다.
그러므로 node.js 객체를 제어하려면 JavaScript로 제어해야 한다.

JavaScript는 자체적으로 가지고 있는 객체들이 있다.
ex. Array
ex. Function
ex. Date 등

Javascript Core vs. JavaScript
JavaScript로 제어할 수 있는 객체들을 Javascript Core라고 한다.
```

---

## 4강 Object Model ::: 이미지 태그 제어하기

#### Object Model이란 무엇인가

+ JavaScript로 브라우저를 제어할 수 있도록 브라우저의 여러 구성요소들을 객체로 만들어 놓은 것이다.

#### 이미지 태그 객체를 변수로 선언하기

+ html 파일을 아래와 같이 만든다.

```
# p_objectmodel.html


<!DOCTYPE html>
<html>
<head>

</head>
<body>
    <img src="https://s3-ap-northeast-1.amazonaws.com/opentutorialsfile/course/94.png" />
</body>
</html>
```

+ html 파일을 브라우저에서 열고, 크롬 개발자도구의 console 창에 다음과 같이 한 줄씩 입력해본다.

```
# 크롬 개발자도구 console


> var imgs = document.getElementByTagName('img');
> imgs
> imgs[0]
<img src="https://s3-ap-northeast-1.amazonaws.com/opentutorialsfile/course/94.png">
```
```
# 위 코드 설명

var imgs : imgs라는 변수를 선언한다.
document.getElementByTagName('img') : document 객체에서 img라는 태그이름을 가진 요소들(plural)을 가져온다.
imgs : imgs는 Elements를 가져오므로 원소를 여러 개 가질 수 있는 배열이다.
img[0] : imgs 배열의 첫 번째 원소를 return한다.
```

#### 이미지 태그 객체를 수정해보기

+ JavaScript를 통해 이미지 태그 객체에 style을 넣어보자.

```
# console

> imgs[0].style.width='300px';
"300px"
```

+ 크롬 개발자도구의 Elements 탭으로 가서 html 파일을 보면 img 태그에 style 값이 추가된 것을 확인할 수 있다.

```
# html 파일

<img src="https://s3-ap-northeast-1.amazonaws.com/opentutorialsfile/course/94.png" style="width: 300px;">
```

---

## 3강 script 파일을 어디에 위치시켜야 좋은가

#### 결론

+ body 태그가 끝나는 곳에 위치시키는 것이 바람직하다.

#### head 태그 vs. body 태그

+ head 태그의 기능
    + 웹 페이지에 사용되는 여러 가지 리소스들을 load하거나
    + 웹 페이지를 설명하는 용도

+ body 태그의 기능
    + 웹 페이지에 표현될 HTML 요소를 담아두는 용도

#### head 태그에 script 파일을 위치하면 생기는 오류

```
<head>
    <script>
        var hw = document.getElementById('hw');
        hw.addEventListner('click', function(){
            alert('Hello, World');
        })
    </script>
</head>
<body>
    <input type="button" id="hw" value="Hello, World" />
</body>
```

+ HTML 파일은 코드를 위에서 아래로 실행한다.
+ `<head>` 태그에서 `<script>` 태그 내용을 실행한다.
+ `<script>`가 참조하는 태그의 내용 `id='hw'`가 `<body>` 태그 안에 있다.
+ 참조된 값은 아직 읽혀지지 않았으므로 `hw = null`이 된다.
+ `<script>` 코드의 내용이 `null`(존재하지 않는 것)에 대해 실행하게 된다.
+ 에러가 발생한다.

#### head 태그에 script 파일을 위치시켜도 에러를 발생하지 않도록 하는 방법

```
<head>
    <script>
        window.onload = function(){
            var hw = document.getElementById('hw');
            hw.addEventListner('click', function(){
                alert('Hello, World');
            })
        }
    </script>
</head>
```
+ `window.onload = function(){}` 안에 `<script>`코드를 넣으면
+ 모든 HTML 요소가 다 실행된 이후에 JavaScript 코드를 실행한다.
+ `onload`는 현재 웹 페이지에 있는 모든 코드가 다 읽힌 후에 함수를 실행한다는 뜻이다.

#### body 태그에 script 파일을 위치시키는 것이 바람직한 이유

+ 성능이 빠르기 때문이다.
    + head 태그에서 script 파일을 로딩하는 경우 사용자 입장에서는 rendering이 지연되므로 웹 페이지가 하얗게 보일 수 있다.
    + body 태그 끝에서 script 파일을 로딩하는 경우 순서대로 코드를 읽으면 되므로 rendering이 지연되지 않는다.

---

## 2강 HTML에서 JavaScript를 로드하는 방식

#### inline

```
<input type="button" onclick="alert('Hello, World')" value="Hello, World" />
```

+ `onclick` : JavaScript를 실행하는 HTML의 속성
    + 코드 읽는 법
        + `onclick`이 포함된 태그를 사용자가 클릭했을 때
        + `onclick`의 값으로 들어가 있는 JavaScript를 실행한다.

> `onclick`은 html 언어이지만, `onclick`의 값은 JavaScript 언어이다.

+ 단점 : 정보와 제어를 구분하지 않는다.
    + 정보와 제어가 한 곳에 표현되어 있어서 유지 및 보수가 어렵다.
    + HTML 코드 따로, JavaScript 코드 따로 모여있는 것이 편하다.

#### script

```
<input type="button" id="hw" value="Hello, World" />
<script type="text/JavaScript">
    var hw = document.getElementById('hw');
    hw.addEventListner('click', function(){
        alert('Hello, World');
    })
</script>
```

+ `<input>`태그 안에 `onclick`이라는 속성이 사라졌다.

+ `<script>` 태그가 등장했다.
    + `<script>` 태그 안에 JavaScript 코드가 들어간다.

+ `getElementById` : Element란 HTML 태그를 의미한다.

> `<script>` 태그의 속성인 `type="text/JavaScript"`는 HTML5부터는 없어도 된다.

+ 장점 : 정보와 제어를 구분한다.
    + HTML 코드 안에 JavaScript 코드가 존재하지 않아서 유지 및 보수가 쉽다.
    + JavaScript 코드를 수정할 때는 `<script>` 태그만 살펴보면 된다.

#### 외부 파일로 분리

```
# practice/p_script.html

<script src="./script.js"></script>
```

```
# practice/script.js

var hw = document.getElementById('hw');
hw.addEventListener('click', function(){
    alert('Hello, World');
})
```

+ `src="./"`: 현재 파일과 같은 디렉토리에서 소스를 참조한다.
+ html 파일 안에 JavaScript 코드가 완전히 사라졌다.

+ 장점 : 정보와 제어를 완전히 구분하고, 유지 및 보수의 편의성이 극대화된다.
    + HTML 문서에서 JavaScript 코드를 완전히 바깥 쪽으로 몰아낼 수 있다.
    + 똑같은 .js 파일을 여러 개의 html 파일이 공통적으로 참조하고 있다면 코드의 중복을 없앨 수 있다.
    + .js 파일을 별도로 빼내게 되면 브라우저에 의해서 캐시가 되므로 중복 다운로드 받을 필요가 없어진다.

> 캐시(cache)
>
> + 브라우저에 표시하기 위해 웹 서버(server)에서 사용자의 하드디스크(client)로 다운로드 받은 파일
> + 네트워크의 전송속도로 인한 지연현상(latency)을 현저하게 낮출 수 있다.

---

## 1강 HTML vs. CSS vs. JavaScript

+ HTML : 정보를 표현한다.
+ CSS : 정보를 미적으로 꾸며준다.
+ JavaScript : HTML을 동적으로 제어한다.

---
