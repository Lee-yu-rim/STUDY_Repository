image & hiperlink
===
1. 이미지 삽입하기
- 절대경로를 이용한 이미지 삽입
```js
<img src="C:\work\htmlcssworkspace\sea.jpeg"/>
//사진이 있는 곳의 경로를 직접 입력
```

- 상대경로를 이용한 이미지 삽입
```js
//동위(같은 위치에 파일이 있을 경우)
//- 파일이름만 입력
<img src="sea.jpeg"/>

//상위(이미지 파일이 html파일의 상위 폴더 안에 위치할 경우)
//../를 입력하여 파일 위치까지 올라감
<img src="../sea.jpeg"/>

//하위(이미지 파일이 html파일의 하위 폴더 안에 위치할 경우)
//파일이 위치한 폴더명\파일명 입력
<img src="images\sea.jpeg"/>

//이미지 링크(url)를 통한 삽입
<img src="이미지링크"/>
```
***
2. 하이퍼링크 삽입하기
```js
<a href="파일위치(상대/절대), url">화면에 출력되는 부분</a>
```

```js
<a href="tag.html" target="_self">링크</a>

//이미지에 링크 걸기
<a href="https://www.naver.com/"><img src="naver.png"/></a>

//한페이지 내에서 문서 이동
<a href="#content">내용</a>

<a id="content">내용 위치</a>

<a href="#top">맨위로</a>

//이미지에 특정 영역에만 링크 걸기
<img src="cat.jpg" usemap="#cutecat"/>
<map name="cutecat">
    <area shape="모양" coords="좌표값" href="링크주소" target="_blank"/>
```
