HTML Tag
====
1. 텍스트에 관련된 태그들

- 원하는 형식으로 글 표현 

<pre>
    내가 그의 이름을 불러 주기 전에는
    그는 다만 
    하나의 몸짓에 지나지 않았다.

    내가 그의 이름을 불러 주었을 때 
    그는 나에게로 와서
    꽃이 되었다.
</pre>


- 공백 표현 태그   
이&nbsp;&nbsp;&nbsp;유&nbsp;&nbsp;&nbsp;림


- 글자 강조 태그   
<strong>글자강조</strong>


- 글자 기울임 태그   
<em>글자기울임</em>   
<i>이태릭체</i>


- 인용구문 태그   
<q>인용구문</q>


- 형광펜 태그   
<mark>형광펜</mark>


- 영역 태그   
<span>일부 영역에 효과를 주기 위해 사용</span>

- 목록 표시 태그   
    - 기호를 이용한 표현
    <ul>
        <li>1</li>
        <li>2</li>
    </ul>   

    - 순서를 이용한 표현
    <ol>
        <li>1</li>
        <li>2</li>
    </ol>

    -타입 지정하여 표현
    <ol type="a">
        <li>1</li>
        <li>2</li>
    </ol>   


- 용어 설명 표현(계층구조)   
<dl>
    <dt>hello</dt>
    <dd>
        설명하는 내용
    </dd>
</dl>

***

2. 테이블 태그
<!-- 2행 3열 테이블 -->
<figure>
    <figcaption>
        테이블 제목
    <figcaption>
    <table border="1px" height="100" width="100px"> 
        <tr>
            <td>1</td><td>2</td><td>3</td>
        </tr>
        <tr>
            <th>1</th><th>2</th><th>3</th>
            <!-- th : 가운데 정렬 -->
        </tr>
    </table>
</figure>


- 셀병합
<table border="1px" height="100" width="100px"> 
        <tr>
            <td rowspan="2">1</td><td colspan="2">2</td>
            <!-- rowspan : 행병합 / colspan : 열병합 -->
        </tr>
        <tr>
            <th>1</th><th>2</th>
            <!-- th : 가운데 정렬 -->
        </tr>
    </table>


