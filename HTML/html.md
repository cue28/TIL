# HTML (Hypertext Markup Language)

## HTML5 페이지 구조
`<html lang='ko'>` : 실제 웹 브라우저가 동작하는 데 어떠한 영향도 끼치지 않지만, 검색 엔진이 웹 페이지를 탐색할 때 해당 웹 페이지가 어떠한 언어로 만들어져 있는지 쉽게 인식하게 만든다.

`<title></title>` : 검색 엔진에게 웹 페이지의 제목과 관련된 정보를 부는 데 사용되므로 입력하는 것이 좋다.

## 글자 태그

**제목**
- `<h1> ~ <h6>`
- heading, 각 숫자는 크기 및 우선 순위를 나타낸다.
- 폰트를 강제로 지정한다.

**본문**
- `<p>` : paragraph, 단락, 하나의 단락을 만들 수 있다. 
- `<br>` : 줄바꿈 태그
- `<hr>` : 수평 줄 태그

**앵커 태그**
- `<a>`
- HTML의 H는 하이퍼텍스트로 사용자의 선택에 따라 특정한 정보와 관련된 부분으로 이동할 수 있게 조직화된 문서를 의미한다. HTML 웹 페이지가 조직화된 문서 형태를 가질 수 있는 이유는 앵커 태그이기 때문이다. 
- 서로 다른 웹 페이지 사이를 이동하거나 웹 페이지 내부에서 특정한 위치로 이동할 때 사용하는 태그이다.
- 다음과 같이 자주 사용된다.

```html
<div>
  <a href="#">언론사 전체보기</a>
  <ul>
    <li><a href="#">종합지</a></li>
    <li><a href="#">경제지</a></li>
    <li><a href="#">스포츠/연예</a></li>
    <li><a href="#">지역지</a></li>
  </ul>
</div>
```
- 페이지 내부 이동도 가능하다.
- 원하는 장소에 id 속성을 부여해야한다. id 속성을 부여하고 a 태그의 href 속성에 # 아이디 형태의 문자열로 입력한다.
```html
<a href="#alpha"></a>
<h1 id="alpha"></h1>
<p>alpha</p>
```

**글자 형태**
- 글자 형태 태그를 사용해 웹 페이지의 글자에 형태와 의미를 부여한다.
- `<b>` : 굵은 글자 태그
- `<i>` : 기울어진 글자 태그
- `<small>` : 작은 글자 태그
- `<sub>` : 아래에 달라 붙는 글자 태그
- `<sup>` : 위에 달라 붙는 글자 태그
- `<ins>` : 밑줄 글자 태그
- `<del>` : 가운데 줄이 그러진 글자 태그
- 스타일시트로 처리하므로 최근에는 잘 사용하지 않는다.

**루비 문자**
- 일본어에서 자주 사용되는 글자 형식으로 한자 위에 표시되는 글자를 의미한다.
- 한국어에도 한자어가 많으므로 사용할 수 있는 태그
- `<ruby>` : 루비 문자 선언 태그
- `<rt>` : 위에 위치하는 작은 문자 태그
- `<rp>` : ruby 태그를 지원할 경우 출력되지 않는 태그
- 지원하지 않는 웹 브라우저도 있음 -> 태그가 정산적으로 출력될 수 있게 만드는 태그가 rp 태그이다.

```html
<ruby>
  <span>대한민국</span>
  <rt>大韓民國</rt>
</ruby>

//지원하지 않는 웹 브라우저
<ruby>
  <span>대한민국</span>
  <rp>(</rp>
  <rt>大韓民國</rt>
  <rp>)</rp>
</ruby>
```

## 목록 태그
웹 페이지에 빼놓고 등장하는 요소가 있다면 바로 메뉴이다. 일반적으로 페이지를 이동할 떄 사용되는 메뉴를 내비게이션 메뉴라고 부릅니다. 이때 사용하는 태그들입니다.

- `<ul>` : 순서가 없는 목록 태그 -> 글머리에 기호가 붙음
- `<ol>` : 순서가 있는 목록 태그 -> 1,2,3번호가 매겨짐
- `<li>` : 목록 요소
- 중첩된 목록도 사용가능하다.

```html
<!DOCTYPE html>
<html>
<head>
    <title>HTML TEXT Basic Page</title>
</head>
<body>
    <h1>ol tag</h1>
    <ol>
        <li>Facebook</li>
        <li>Tweeter</li>
        <li>Linked In</li>
    </ol>
    <h1>ul tag</h1>
    <ul>
        <li>Facebook</li>
        <li>Tweeter</li>
        <li>Linked In</li>
    </ul>
</body>
</html>
```

**정의 목록**
- 특정 용어와 그 정의를 표현할 때 사용하는 태그이다.
- 단어를 써놓고 그 정의를 풀이한 목록을 정의 목록이라고 한다.
- `<dl>` : 정의 목록 태그 (definition list)
- `<dt>` : 정의 용어 태그 (definition term)
- `<dd>` : 정의 설명 태그 (definition description)

```html
<body>
    <dl>
        <dt>HTML5</dt>
        <dd>Multimedia Tag</dd>
        <dd>Connectivity</dd>
        <dd>Device Access</dd>
        <dt>Milk</dt>
        <dd>Animation</dd>
        <dd>3D Transform</dd>
    </dl>
</body>
```

## 테이블 태그

**테이블 태그 기본**
- HTML 페이지에서 표를 만들 때 사용하는 태그이다.
- 표를 만들 때는 table 태그를 사용한다.
- `<tr>` : 표 내부의 행 태그 table row
- `<th>` : 행 내부의 제목 셀 태그 table header
- `<td>` : 행 내부의 일반 셀 태그 table data

```html
    <table border="1">
        <tr>
            <th>Header 1</th>
            <th>Header 2</th>
        </tr>
        <tr>
            <td>Data 1</td>
            <td>Data 1</td>
        </tr>
        <tr>
            <td>Data 2</td>
            <td>Data 2</td>
        </tr>
    </table>
```

- 계층 구조를 형성하며, tbody 태그가 자동으로 생성된다.
- caption, colgroup, thead, tbody, tfoot 등의 태그도 넣을 수 있지만 이는 테이블 태그들이 익숙해지면 살펴보자!

**태이블 태그의 속성**

- table 태그는 속성이 굉장히 많았다. 하지만 HTML5의 table 태그는 속성 하나만 가지고 있다.
- border : 표의 테투리 두께를 지정
- rowspan : 셀의 높이 지정
- colspan : 셀의 너비 지정

## 이미지 태그
- `<img>`
- src : 이미지의 경로 지정
- alt : 이미지가 없을 때 나오는 글자 지정 (필수! 오류 시 대체 텍스트, 검색 엔진 노출)
- width : 이미지의 너비 지정
- height : 이미지의 높이 지정

웹 페이지 디자인 시 참고 : 안에 텍스트는 Lorem ipsum / http://placehold.it 원하는 크기의 이미지 제공

## 오디오 태그
웹 브라우저에서 플러그인의 도움 없이 음악을 재생할 수 있게 만들어주는 HTML5 태그입니다. 

**audio 태그**
```html
<body>
    <audio src="Kalimba.mp3" controls="controls"></audio>
</body>
```
- src : 음악 파일의 경로 지정
- preload : 음악을 재생하기 전에 모두 불러올지 지정
- autoplay : 음악을 자동 재생할 지 지정
- loop : 음악을 반복할지 지정
- controls : 음악 재생 도구를 출력할지 지정

**source 태그**
- 브라우저마자 지원하는 확장자 형식이 다르기 떄문에 나타나는 문제를 해결하기 위해 나온 태그
```html
<body>
    <audio controls="controls">
        <source src="Kalimba.mp3" type="audio/mp3" />
        <source src="Kalimba.ogg" type="audio/ogg" />
    </audio>
</body>
```
- type 설정을 필수 ! 속성을 입력하지 않으면 웹 브라우저가 음악 파일을 내려받은 뒤에 재생 가능한 파일인지 확인하므로 트래픽 낭비가 된다.

## 비디오 태그
- 웹 페이지에서 동영상을 볼 수 있게 만들어준다.

**video 태그**
- src : 파일 경로
- poster : 비디오 준비 중일 때 이미지 파일 경로 지정 (썸네일)
- preload : 비디오를 재생하기 전에 모두 불러올지 지정
- auto : 자동 재생
- loop : 반복 지정
- controls : 비디오 재생 도구 출력할지 지정
- width : 비디오 너비 지정
- height : 높이 지정
- 마찬가지로 웹 브라우저마다 지원하는 형식이 달라 source 태그를 사용해야한다.

```html
<video poster="http://placehold.it/640x360" width="640" height="360" controls="controls">
    <source src="Wildlife.mp4" type="video/mp4" />
    <source src="Wildlife.webm" type="video/webm" />
</video>
```
- 브라우저마자 video 형태가 일관되지 않으므로 웹 페이지를 디자인할 때 문제가 될 수 있다. 
- 문제 해결 : video.js 플러그인 (다음에 자세히 살펴보도록 하자 ! p.74)

## 입력 양식 태그
- 사용자에게 입력받은 공간
- 입력 양식을 만들 때 사용

**입력 양식 개요**
- `<form>` 
```html
<form>
    <input type="text" name="search" />
    <input type="submit" />
</form>
```
- 데이터를 입력하고 쿼리 전송 버튼을 누르면, 데이터가 지정된 장소에 지정된 방법으로 전달된다.
- action : 입력 데이터의 전달 위치를 지정한다.
- method : 입력 데이터의 전달 방식을 선택한다.

