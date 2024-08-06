<p>selenium을 연습하면서 서울시 주유소를 대상으로 셀프 주유소가 저렴한지 확인해보려고 한다. </p>
<blockquote>
<p>💡 <strong>Beautiful Soup 만으로 해결할 수 없는 것</strong>
접근할 웹 주소를 알 수 없을 때
자바스크립트를 사용하는 웹페이지, 동적 페이지(ex. 무한스크롤)
웹 브라우저로 접근하지 않으면 안될 때(ex. form 입력에 따른 페이지 이동)</p>
</blockquote>
<p>이런 <code>Beautiful Soup</code> 의 한계를 <code>Selenium</code> 으로 해결</p>
<h1 id="selenium">Selenium</h1>
<ul>
<li>웹 브라우저를 원격 조작하는 도구</li>
<li>자동으로 URL을 열고 클릭 등이 가능</li>
<li>스크롤, 문자의 입력, 화면 캡처 등등</li>
<li>브라우저에서의 자바 스크립트 코드 실행 가능</li>
</ul>
<h2 id="세팅">세팅</h2>
<h3 id="python-모듈-설치">python 모듈 설치</h3>
<pre><code class="language-bash">conda install conda-forge::selenium</code></pre>
<h3 id="chrome-driver-설치">Chrome driver 설치</h3>
<p>원래는 chrome driver를 따로 설치해줘야하는데, selenium 업데이트로 chrome driver를 따로 설치 안해줘도 됨.</p>
<h3 id="세팅-확인">세팅 확인</h3>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/8859f154-3dde-4e3f-9b82-be7cf15fd37b/image.png" /></p>
<p>이 코드를 실행했을 때, </p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/ce0909f0-b0c7-4425-9087-ede66aa978ab/image.png" /></p>
<p>이런 창이 뜨면 세팅 완료</p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/95ac83f2-b8cb-4036-ba37-5255f5b82c91/image.png" /></p>
<p>driver.quit()을 하면 드라이버로 열었던 창이 닫힘과 동시에 드라이버가 동작 정지(드라이버 자원 반납)</p>
<h2 id="기초">기초</h2>
<p><a href="https://nbviewer.org/github/solpinetree/ds_study/blob/main/source_code/04.%20Selenium_Basic_1.ipynb">selenium 기초 연습 예제</a></p>
<p><br /><br /></p>
<h1 id="셀프-주유소는-정말-저렴할까">셀프 주유소는 정말 저렴할까?</h1>
<h2 id="데이터-확보">데이터 확보</h2>
<p><a href="https://www.opinet.co.kr/searRgSelect.do">싼 주유소 찾기 Opinet</a>에 가면 주유소 유가 정보를 확인 가능 
여기서 <code>브랜드</code>, <code>가격</code>, <code>셀프 주유 여부</code>, <code>위치</code> 정보를 얻어서 분석을 하고자 한다. </p>
<h3 id="페이지-접근">페이지 접근</h3>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/0a3bad56-a8f5-4577-bfcc-8eb671d50497/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/82647594-7640-44a3-9813-b89f35a8639c/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/a4981177-3039-4bb7-a91e-980088dd2a17/image.png" /></p>
<p>왼쪽 상단의 지역 selector 를 조작해서 서울에 있는 데이터들을 조회 가능</p>
<h3 id="시도-설정">시/도 설정</h3>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/f77d5edd-0f78-4a88-887e-ca2fa25f9e4f/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/64e8bd88-9728-4b71-9f54-c3ba24b3556d/image.png" /></p>
<p><code>서울특별시</code> 가 sido_names[0]이므로</p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/f712d572-3eee-4d9d-b887-bcb9859da35d/image.png" /></p>
<h3 id="구-설정">구 설정</h3>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/de6d92fa-24f5-4d51-b4fd-f42700a41bb6/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/75d6ba9a-ce70-4f2c-bb9a-c2b5ae29fb68/image.png" /></p>
<p>일단 관악구를 선택해봤다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/582cb7db-1c80-4ba9-a737-67cc1e2effce/image.png" /></p>
<h3 id="데이터-엑셀-저장">데이터 엑셀 저장</h3>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/b5a4767a-f2ab-470d-9a85-aab7a9757f66/image.png" /></p>
<p>홈페이지에서는 조회한 데이터 엑셀 저장 기능도 제공하는데, 서울시의 유가 데이터를 엑셀로 저장해서 분석하기 위해 엑셀 저장 버튼을 클릭해야한다. </p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/98cfb46f-be62-4829-99a1-2c2c1f4cf851/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/608336ae-2a87-4738-942b-c053c84a7d76/image.png" /></p>
<h3 id="서울시-모든-구의-데이터-엑셀-저장">서울시 모든 구의 데이터 엑셀 저장</h3>
<p>위에서 한 과정을 서울시 구의 개수만큼 for문을 돌려 모든 구의 데이터 엑셀을 다운로드 받는다. </p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/104497c6-8112-4913-bca0-b4c3efe7506c/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/2bff4746-c502-41d6-9284-80ffce4c1d82/image.png" /></p>
<p><br /><br /></p>
<p><a href="https://nbviewer.org/github/solpinetree/ds_study/blob/main/source_code/04.%20Self%20Oil%20Station%20Price%20Analysis.ipynb">전체 코드 확인</a></p>
<p><br /><br /><br /><br /></p>
<blockquote>
<p>이 글은 제로베이스 데이터 취업 스쿨의 강의 자료 일부를 발췌하여 작성되었습니다.</p>
</blockquote>