<p>python, pandas, matplotlib 등을 공부하기 위해 서울시 CCTV 현황 데이터 분석을 한다.</p>
<h2 id="목표">목표</h2>
<p>서울시 자치구별 인구수 대비 cctv 개수에 대해 시각화를 한다.</p>
<h2 id="상세-과정목표">상세 과정(목표..?)</h2>
<ol>
<li>서울시 구별 CCTV 현황 데이터 확보</li>
<li>인구 현황 데이터 확보</li>
<li>CCTV 데이터와 인구 현황 데이터 합치기</li>
<li>데이터를 정리하고 정렬</li>
<li>그래프 도출</li>
<li>전체적인 경향 파악</li>
<li>경향에서 벗어난 데이터 확인</li>
</ol>
<h2 id="1-서울시-구별-cctv-현황-데이터-확보">1. 서울시 구별 CCTV 현황 데이터 확보</h2>
<p>구글에 '<code>서울시 자치구 연도별 cctv 설치 현황</code>' 라고 검색하고,
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/326e2d34-6aef-47b4-ad37-56330adc3485/image.png" />
최상단에 뜨는 링크를 검색해서 들어가서 데이터를 다운로드 받았다. </p>
<h2 id="2-인구-현황-데이터-확보">2. 인구 현황 데이터 확보</h2>
<p>또 구글에서 '서울시 주민등록인구 구별 통계' 라고 검색하고, 
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/180fc42c-7986-4622-b476-beb4e9e9d450/image.png" />
최상단에 뜨는 링크를 검색해서 다운로드 받았다.</p>
<h2 id="3-cctv-데이터와-인구-현황-데이터-합치기">3. CCTV 데이터와 인구 현황 데이터 합치기</h2>
<h3 id="pandas로-csv-엑셀-파일-읽기">Pandas로 CSV, 엑셀 파일 읽기</h3>
<pre><code>📝 pandas
    - python 에서 R 만큼의 강력한 데이터 핸들링 성능을 제공하는 모듈
    - 단일 프로세스에서는 최대 효율
    - 누군가는 스테로이드 맞은 엑셀로 표현하기도 한다고..</code></pre><p>먼저, pandas 를 import 한다.
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/74dfbcfb-8964-4fff-8e0d-cc99ca127e6f/image.png" /></p>
<p>그 다음, 서울시 CCTV 데이터를 pandas 로 읽는다.</p>
<details>
read_excel(..) 에서 openpyxl 을 설치하라는 에러가 났음
<div>

<p>xlrd 를 설치해도 해결이 안돼서 openpyxl 를 설치하니 해결됐다.
pandas 기본 엔진이었떤 xlrd가 업데이트되면서 xlsx를 지원하지 않아서 그렇다고 한다.
(출처 : <a href="https://steadiness-dev-invest.tistory.com/141">https://steadiness-dev-invest.tistory.com/141</a>)</p>
</div>
</details>

<details>
read_csv(..) 한글이 깨진다면, 인코딩 설정
<div>

<pre><code class="language-python">  pd.read_csv(&quot;경로&quot;, encoding=&quot;utf-8&quot;)</code></pre>
</div>
</details>

<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/a381b67d-96f4-4170-be14-ec63782f8068/image.png" /></p>
<p>0번째 행과 0번째 열에 아무런 값이 없어서 제외해서 다시 가져왔다. (미리 엑셀 보기)</p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/cd4c32a1-a930-405c-bd83-b68ee05ed27b/image.png" /></p>
<p>구 이름을 나타내는 컬럼명이 &quot;구분&quot;으로 되어있는데 이를 &quot;구별&quot;로 바꾸면 더 이해하기 쉬울 것 같아 수정한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/74a7e5d5-5896-46a0-8443-360605d5ef59/image.png" /></p>
<p>이제 넘어가서, 서울시 인구현황 데이터를 pandas 로 읽는다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/efff00c8-19a1-480c-8ca4-db41ed483cc1/image.png" /></p>
<p>컬럼명을 간단하게 바꿔준다. </p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/5541e1ad-e649-4029-ac13-b90fa43fba93/image.png" /></p>
<p>.. 작성 중</p>