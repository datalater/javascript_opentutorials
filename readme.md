copyright ⓒ JMC 2017

주요 소스: 생활코딩 Javascript on Web Browser

## 4강: Browser Object Model

resume : https://www.youtube.com/watch?v=5fq79_X_yKo&index=8&list=PLuHgQVnccGMDTAQ0S_FYxXOi1ZJz4ikaX

## 3강: script 파일을 어디에 위치시켜야 좋은가

#### head 태그 vs. body 태그

+ head 태그의 기능
    + 웹 페이지에 사용되는 여러 가지 리소스들을 load하거나
    + 웹 페이지를 설명하는 용도

+ 결론
    + body 태그가 끝나는 곳에 위치시키는 것이 바람직하다.

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
> `<script src=./script.js></script>` == `<script> var hw ... </script>`

+ HTML 파일은 코드를 위에서 아래로 실행한다.
+ `<head>` 태그에서 `<script>` 태그 내용을 실행한다.
+ `<script>`가 참조하는 태그의 내용이 `<body>` 태그 안에 있다.
+ 참조된 값은 아직 아래에 있어서 읽지 않았으므로 `null`이 된다.
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
+ `window.onload = function(){}` :
    + `onload` : 현재 웹 페이지에 있는 모든 코드가 다 읽힌 후에 함수를 실행한다.
    + 따라서, function() 안에 javascript 코드를 넣으면
    + 모든 HTML 요소가 다 실행된 이후에 javascript 코드를 실행한다.

#### body 태그에 script 파일을 위치시키는 것이 바람직한 이유

+ 성능이 빠르다.
    + head 태그에서 script 파일을 로딩하는 경우 사용자 입장에서는 rendering이 지연되므로 웹 페이지가 하얗게 보일 수 있다.

---

## 2강: HTML에서 javascript를 로드하는 방식

#### inline

```
<input type="button" onclick="alert('Hello, World')" value="Hello, World" />
```

+ `onclick` : javascript를 실행하는 HTML의 속성
    + 코드 읽는 법
        + `onclick`이 포함된 태그를 사용자가 클릭했을 때
        + `onclick`의 값으로 들어가 있는 javascript를 실행한다.

> `onclick`은 html 언어이지만, `onclick`의 값은 javascript 언어이다.

+ 단점 : 정보와 제어를 구분하지 않는다.
    + 정보와 제어가 한 곳에 표현되어 있어서 유지 및 보수가 어렵다.
    + HTML 코드 따로, javascript 코드 따로 모여있는 것이 편하다.

#### script

```
<input type="button" id="hw" value="Hello, World" />
<script type="text/javascript">
    var hw = document.getElementById('hw');
    hw.addEventListner('click', function(){
        alert('Hello, World');
    })
</script>
```

+ `<input>`태그 안에 `onclick`이라는 속성이 사라졌다.

+ `<script>` 태그가 등장했다.
    + `<script>` 태그 안에 javascript 코드가 들어간다.

+ `getElementById` : Element란 HTML 태그를 의미한다.

> `<script>` 태그의 속성인 `type="text/javascript"`는 HTML5부터는 없어도 된다.

+ 장점 : 정보와 제어를 구분한다.
    + HTML 코드 안에 javascript 코드가 존재하지 않아서 유지 및 보수가 쉽다.
    + javascript 코드를 수정할 때는 `<script>` 태그만 살펴보면 된다.

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
+ html 파일 안에 javascript 코드가 완전히 사라졌다.

+ 장점 : 정보와 제어를 완전히 구분하고, 유지 및 보수의 편의성이 극대화된다.
    + HTML 문서에서 javascript 코드를 완전히 바깥 쪽으로 몰아낼 수 있다.
    + 똑같은 .js 파일을 여러 개의 html 파일이 공통적으로 참조하고 있다면 코드의 중복을 없앨 수 있다.
    + .js 파일을 별도로 빼내게 되면 브라우저에 의해서 캐시가 되므로 중복 다운로드 받을 필요가 없어진다.

> 캐시(cache)
>
> + 브라우저에 표시하기 위해 웹(server)에서 사용자의 하드디스크(client)로 다운로드 받은 파일
> + 네트워크의 전송속도로 인한 지연현상(latency)을 현저하게 낮출 수 있다.

---

## 1강: HTML vs. CSS vs. Javascript

+ HTML : 정보를 표현한다.
+ CSS : 정보를 미적으로 꾸며준다.
+ Javascript : HTML을 동적으로 제어한다.
