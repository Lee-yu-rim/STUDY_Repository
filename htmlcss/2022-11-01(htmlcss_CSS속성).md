CSS의 속성
===
- 글꼴 속성 : font-family
```
.fontstyle {
    font-family: 궁서;
}
```

- 웹폰트
```
@import url(글꼴 주소)
.fontstyle {
    font-family: '글꼴 이름', cursive;
}
```

- 글자 크기:font-size
    - 절대 크기 : px , pt
    - 상대 크기 : em , %  // 1em = 100%
```
p {
    font-size: 1em;
}
```


- 글자 굵기 : font-weight
```
p {
    font-weight: bold;
}
```

- 글자 스타일 : font-style
```
p {
    font-style: italic;
}
```

- 글자 색상 : color
```
p {
    color: red;
}
```

- 글자 밑줄 : text-decoration
```
p { 
    text-decoration: underline;  //none, overline, line-through
}
```

- 글자 그림자 효과 :text-shadow
    - text-shadow: 가로이동거리 세로이동거리 번짐정도 그림자색상
```
.shadow {
    text-shadow: 5px 5px 3px black;
}
```

- 글자 간격(자간) : letter-space
```
.letter { 
    letter-spacing: 0.5em;
}
```

- 공백과 줄바꿈 : white-space
    - white-space: normal | nowrap | pre | pre-wrap | pre-line
```
.normal {white-space: normal;}
.nowrap {white-space: nowrap;}
.pre {white-space: pre;} 
.prewrap {white-space: pre-wrap;} 
.preline {white-space: pre-line;}
```
|nowrap|pre|pre-wrap|pre-line|
|:----:|:-:|:------:|:------:|
|공백 x|공백 o|공백 o|공백 x|
|줄바꿈 x|줄바꿈 x|줄바꿈 o|줄바꿈 o|

<hr>

- 텍스트 정렬(수평) : text-align
    - text-align: left | right | center | justify
```
.left {text-align: left;}   왼쪽 정렬
.right {text-align: right;}   오른쪽 정렬
.center {text-align: center;}   가운데 정렬
.justify {text-align: justify;}   양쪽 정렬(균등분배) 
```
- 줄(행) 간격 : line-height
```
.line{
    line-height: 2em;
}
```
- 글자가 넘치는 기능 제어 : text-overflow
    - overflow -> nowrap | hidden | ellipsis 3가지를 모두 사용해야함
```
p {
    white-space : nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}