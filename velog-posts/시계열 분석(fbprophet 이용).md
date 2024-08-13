<blockquote>
<p>💡 <strong>시계열 데이터</strong>
시간의 흐름에 대해 특정 패턴과 같은 정보를 가지고 있는 경우</p>
</blockquote>
<blockquote>
<p>💡 <strong>Seasonal Time Series</strong>
주기성을 가지고 있는 데이터</p>
</blockquote>
<h2 id="fbprophet-설치">fbprophet 설치</h2>
<ul>
<li>페이스북에서 공개한 시계열 예측 라이브러리</li>
<li>정확도가 높고 빠르며 직관적인 파라미터로 모델 수정이 용이함
<a href="https://hyperconnect.github.io/2020/03/09/prophet-package.html">참고</a></li>
</ul>
<blockquote>
<p>🤔 *<em>This is a python-holidays entity loader class. For entity inheritance purposes please import a class you want to derive from directly: e.g., <code>from holidays.countries import Entity</code> or <code>from holidays.financial import Entity</code>. 에러 *</em></p>
</blockquote>
<pre><code class="language-python">from fbprophet import Prophet </code></pre>
<p>했더니 에러 남. 
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/3bc2dc98-5a90-4fe5-940f-a2ce77fb56e7/image.png" /></p>
<pre><code class="language-bash">pip install fbprophet </code></pre>
<p>-&gt; conda install 보다 pip install 하면 해결된다.</p>
<br />

<h2 id="웹-유입량-데이터-분석">웹 유입량 데이터 분석</h2>
<p>pinkwink 블로그의 방문자 수를 예측해보고자 한다.</p>
<h3 id="pinkwink-web-traffic-csv-가져와서-전체-데이터-그려보기">pinkwink web traffic csv 가져와서 전체 데이터 그려보기</h3>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/2d7c7eab-27b1-4dd7-b2c2-ce0ce57a6142/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/33012c75-ca8a-4007-b0cf-0571b5ef979e/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/c21d67cb-a47c-4956-a5ac-fd670ca90fa3/image.png" /></p>
<h3 id="트렌드-분석">트렌드 분석</h3>
<h4 id="x축-값fx-생성">x축 값(fx) 생성</h4>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/e907fcb7-112d-4147-9c4a-13c05f50fd2b/image.png" /></p>
<h4 id="에러-계산-함수">에러 계산 함수</h4>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/03dfed9a-7bb3-4b5e-9ebf-c162e0832fbe/image.png" /></p>
<h4 id="시각화">시각화</h4>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/e0da636d-ea8f-4f50-ae61-de79f14dcc94/image.png" /></p>
<h3 id="이후-60일의-방문자-수-예측">이후 60일의 방문자 수 예측</h3>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/53c09c1b-4498-4c29-9431-b1c08a623308/image.png" /></p>
<h4 id="예측-결과에서-상한하한의-범위-포함">예측 결과에서 상한/하한의 범위 포함</h4>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/62551cbd-333d-46ba-a10b-a40717e88af5/image.png" /></p>
<p><br /><br /></p>
<p><a href="https://github.com/solpinetree/ds_study/blob/main/source_code/05.%20forecast.ipynb">전체코드</a></p>
<p><br /><br /></p>
<blockquote>
<p>이 글은 제로베이스 데이터 취업 스쿨의 강의 자료 일부를 발췌하여 작성되었습니다.</p>
</blockquote>