<blockquote>
<p>💡 <strong>Beautiful Soup</strong>
html 및 xml 파일을 파싱하고 탐색하고 수정하는 데 사용됨. 웹 스크래핑 작성을 할 때 매우 유용하며, 웹 페이지에서 원하는 데이터를 추출하는 데 도움이 됨.
<a href="https://nbviewer.org/github/solpinetree/ds_study/blob/main/source_code/03.Web%20Data.ipynb#Beautifulsoup">Beautiful Soup 예제 확인</a></p>
</blockquote>
<p>Beautiful Soup 을 이용해서 <a href="https://www.chicagomag.com/chicago-magazine/august-2024/chicagos-50-best-restaurants-ranked/">시카고 메가진에 실린 시카고 50개 맛집</a> 웹사이트를 스크래핑하고 분석해서 지도 시각화까지 하고자 한다. </p>
<p>메거진 링크를 가면</p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/91a8d8cf-d04b-48b7-ae0a-3668546e38e9/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/8c35c4b2-9b9a-45ae-b4b0-18f114ec8aa5/image.png" /></p>
<p>최고의 50개 식당의 순위, 식당 이름, 식당이 있는 동네 정보가 있다. 
각 식당명을 클릭하면 하위 페이지에 가격의 정도, 가게 주소, 식당 웹사이트 링크도 확인할 수 있다. </p>
<h2 id="메인페이지-분석">메인페이지 분석</h2>
<h3 id="페이지에-연결해서-html-스크랩하기">페이지에 연결해서 html 스크랩하기</h3>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/f06eb2c2-a40c-4fcd-810e-5e52f4ba2bdc/image.png" /></p>
<p>웹 스크래핑을 할 때, 서버가 봇을 차단하지 않도록 <code>User-Agent</code> 를 설정해야하는 경우가 있다. 시카고 매거진도 header 에 User-Agent 를 넘기지 않으면 403 Forbidden response를 반환하므로 User-Agent를 fake_useragent(User-Agent를 알아서 생성해줌) 를 이용해서 넘겨줬다. </p>
<blockquote>
<p>💡 User-Agent
클라이언트의 소프트웨어 및 하드웨어 환경에 대한 정보</p>
</blockquote>
<ul>
<li>실제 크롬에서 시카고 매거진 접속시에 넘기는 User-Agent 값
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/2d922bac-3363-40af-9b47-da8d54fe423b/image.png" /></li>
</ul>
<h3 id="식당-50개-정보-추출">식당 50개 정보 추출</h3>
<h4 id="메인페이지의-html-을-크롬-개발자-도구로-확인">메인페이지의 html 을 크롬 개발자 도구로 확인</h4>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/bdb4eb02-bc5e-4b27-b3b6-e953f059139e/image.png" /></p>
<p>div.br50 안에 a 태그가 50개 존재하는데, 이 a 태그들이 각 순위 하나의 식당 정보들임을 알 수 있었다. </p>
<h4 id="예시로-1위-식당의-순위-동네-하위-링크-이름-추출">예시로 1위 식당의 순위, 동네, 하위 링크, 이름 추출</h4>
<ul>
<li><p>각 a 태그(식당 1개의 태그) 구조
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/d6db97a4-cfa1-4bdd-b680-b0a4faca61af/image.png" /></p>
</li>
<li><p>BeautifulSoup을 이용해서 식당 순위, 동네, 하위 링크, 이름 추출</p>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/e2e5f709-7a16-40f1-9a73-d76f3daa7059/image.png" /></p>
<h4 id="1위-식당-정보-추출을-위해-작성한-코드를-50번-반복해서-50개의-식당-정보를-데이터프레임으로-저장">1위 식당 정보 추출을 위해 작성한 코드를 50번 반복해서 50개의 식당 정보를 데이터프레임으로 저장</h4>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/937d9d47-d5a9-4ec2-a767-926e21e0cd2f/image.png" /></p>
<ul>
<li>컬럼 순서 변경
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/7910d4d9-5c59-489d-ad96-d07ad83f82f7/image.png" /></li>
</ul>
<h4 id="데이터-csv-로-저장">데이터 csv 로 저장</h4>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/2e0bcf69-446b-4efd-b30a-42f18fdf8694/image.png" /></p>
<p><a href="https://nbviewer.org/github/solpinetree/ds_study/blob/main/source_code/03.Web%20Data.ipynb">전체 코드 확인하기</a></p>
<br />
<br />

<blockquote>
<p>이 글은 제로베이스 데이터 취업 스쿨의 강의 자료 일부를 발췌하여 작성되었습니다.</p>
</blockquote>