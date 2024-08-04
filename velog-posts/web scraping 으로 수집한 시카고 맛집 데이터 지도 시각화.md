<blockquote>
<p>💡 <strong>Beautiful Soup</strong>
html 및 xml 파일을 파싱하고 탐색하고 수정하는 데 사용됨. 웹 스크래핑 작성을 할 때 매우 유용하며, 웹 페이지에서 원하는 데이터를 추출하는 데 도움이 됨.
<a href="https://nbviewer.org/github/solpinetree/ds_study/blob/main/source_code/03.Web%20Data.ipynb#Beautifulsoup">Beautiful Soup 예제 확인</a></p>
</blockquote>
<p>Beautiful Soup 을 이용해서 <a href="https://www.chicagomag.com/chicago-magazine/august-2024/chicagos-50-best-restaurants-ranked/">시카고 메가진에 실린 시카고 50개 맛집</a> 웹사이트를 스크래핑하여 지도 시각화까지 하고자 한다. </p>
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
<br />
<br />

<h2 id="하위페이지-분석">하위페이지 분석</h2>
<h3 id="rank1-식당-하위페이지-html-가져와서-정보-추출">rank1 식당 하위페이지 html 가져와서 정보 추출</h3>
<ul>
<li><p>rank1 의 하위 페이지에 있는 식당 정보 확인
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/539ff9dd-1eb9-42e3-8b4f-22e1e5373faa/image.png" />
  가격 정도(비싼 정도), 주소, 웹사이트 정보가 하위페이지에 있다.</p>
</li>
<li><p>위의 부분 html 태그 확인
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/8e4526f5-98b5-4e29-81fe-218a0f9eaf17/image.png" /></p>
</li>
</ul>
<p>확인한 태그에 맞춰 price, address, website 정보를 추출한다.</p>
<ul>
<li><p><code>class=&quot;br50-footer&quot;</code> 수집
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/97ab60b5-106c-4154-9f9c-f75e4e80215e/image.png" /></p>
</li>
<li><p><code>strong</code> tag만 수집
price, address, website 정보가 각 <code>strong</code> 태그 뒤에 붙어 있어서 next_sibling, find_next_sibling 을 이용하면 정보들을 얻을 수 있을 겉 같다.</p>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/f286c075-2e40-42ef-9a0c-41c8639cd1af/image.png" /></p>
<p>이 얻은 <code>strong</code> tag list를 이용해서 price, address, website 정보를 추출한다.</p>
<h4 id="price">price</h4>
<p>가격 정보가 비싼 정도로 되어 있기 때문에 빨간 색 달러표시에 맞게 한국어로 정보를 가지고 있도록 했다.
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/b572c169-4deb-4885-a8b0-3df337c5b902/image.png" /></p>
<p>rank1 식당은 빨간 달러 표시가 3개로 보통의 가격을 가지고 있다. </p>
<h4 id="address">address</h4>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/2cf0e882-805d-49eb-87c4-0bf734e9b1d2/image.png" /></p>
<h4 id="website">website</h4>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/ec242d8c-08dc-42c1-9800-e418ed0b7fbc/image.png" /></p>
<p>이제 위의 코드를 50번 반복해서 식당 50개의 하위 정보들을 수집한다.</p>
<h3 id="50개의-식당-하위-페이지에서-식당-정보-수집">50개의 식당 하위 페이지에서 식당 정보 수집</h3>
<blockquote>
<p>💡 tqdm
for 문 진행상황을 progress bar로 보여준다.
<code>conda install conda-forge::tqdm</code></p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/81e8d936-e2a9-4703-86d5-56ab7c69e94a/image.png" /></p>
<h4 id="수집한-정보-데이터프레임에-컬럼으로-저장">수집한 정보 데이터프레임에 컬럼으로 저장</h4>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/55e7f9e5-b1a8-4885-bd0c-0ba8480791b3/image.png" /></p>
<h4 id="rank를-index로-수정">Rank를 index로 수정</h4>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/528c5c3f-1db6-4380-85bf-efb55bd9f603/image.png" /></p>
<h4 id="url-컬럼-제거">URL 컬럼 제거</h4>
<p>URL 컬럼은 식당들의 하위 페이지에 접근하기 위해 필요했던 것이므로 이제 제거
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/96cda8cd-a3a3-4939-b292-ae6d6b8e36d4/image.png" /></p>
<h4 id="데이터-csv-로-저장-1">데이터 csv 로 저장</h4>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/03b40630-d3f5-4576-bbaa-0b1d41abc2d0/image.png" /></p>
<blockquote>
<p>☑️ <strong>정규표현식 예제</strong>
강의에서는 내가 한 맛집 데이터와 다른 시카고 매거진의 2012년 데이터인 50-best-sandwiches 를 이용하는데, 그 과정에서 정규표현식이 필요한 부분이 있었다. 
<a href="https://nbviewer.org/github/solpinetree/ds_study/blob/main/source_code/03.Web%20Data.ipynb#%EC%A0%95%EA%B7%9C%ED%91%9C%ED%98%84%EC%8B%9D">예제 확인하기</a></p>
</blockquote>
<br />
<br />

<h2 id="지도-시각화">지도 시각화</h2>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/09e53036-41b9-49d0-b266-e948352489d7/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/31acf177-6767-4084-8d69-4931f6ec29a9/image.png" /></p>
<p>구글 geocodding api 사용해서 <code>lat</code>, <code>lng</code> 얻어서 데이터프레임 컬럼에 추가하고 for 문 돌려서 지도에 마커를 찍었다. 
팝업으로는 식당 이름이, 마우스 호버로는 동네가 나오도록 했다. </p>
<p>동네별로 가격의 정도를 두고 분석을 해볼 수도 있을 것 같은데, beautifulsoup과 web scraping 을 위한 토이 프로젝트기에 여기서 마무리를 함.</p>
<br />
<br />


<p><a href="https://nbviewer.org/github/solpinetree/ds_study/blob/main/source_code/03.Web%20Data.ipynb">전체 코드 확인하기</a></p>
<br />
<br />
<br />
<br />

<blockquote>
<p>이 글은 제로베이스 데이터 취업 스쿨의 강의 자료 일부를 발췌하여 작성되었습니다.</p>
</blockquote>