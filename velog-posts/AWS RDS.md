<p>Amazon Relational Database Service
로 AWS에서 제공하는 관계형 데이터베이스 서비스</p>
<p>이 페이지에서는 Cloud 상에 Database를 구축하는 과정을 기록하고자 한다.</p>
<h1 id="rds-생성">RDS 생성</h1>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/405ea5fc-7af7-440d-8ef1-be6169d793ef/image.png" /></p>
<blockquote>
<p>생성하면서 스토리지 자동 조정 활성화는 꼭 off 를 해줘야 함. 
안그러면, 스토리지가 꽉 찼을 때 자동으로 프리티어를 넘어 비용이 부과될 수 있음.
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/8ebc3be5-57cb-4a3f-8dbb-27edc0bc2fff/image.png" /></p>
</blockquote>
<ul>
<li><p>로컬 PC에서 접속해볼 것이므로 퍼블릭 액세스 설정
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/66202bbd-d52c-4b55-acd3-26eba4831a67/image.png" /></p>
</li>
<li><p>자동 백업 off(금방 프리티어 용량이 차버리기 때문)
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/2fb80eb2-6b72-4714-8d2b-13f099e2e9a3/image.png" /></p>
</li>
</ul>
<p><br /><br /></p>
<h1 id="rds-외부-접속">RDS 외부 접속</h1>
<ul>
<li><p>VPC 보안 그룹 클릭
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/a37e4701-47ad-4966-90f1-4f95742b182e/image.png" /></p>
</li>
<li><p>보안 그룹의 인바운드 규칙 수정
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/0cbbbab5-f8cc-40a9-8411-752f5467d718/image.png" /></p>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/cd3d569c-ac71-4d30-aa38-77c296c0d425/image.png" /></p>
<ul>
<li>외부접속 명령어<pre><code class="language-bash">mysql -h &lt;엔드포인트&gt; -P &lt;포트&gt; -u &lt;마스터 사용자 이름&gt; -p</code></pre>
</li>
</ul>
<p><br /><br /></p>
<h1 id="rds-중지">RDS 중지</h1>
<p>750시간이 넉넉하지 않으므로, 사용하지 않을 때는 중지해놓는다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/154edeae-4930-4d40-b28b-1c2280d1cad6/image.png" /></p>
<p>데이터베이스를 클릭하고 작업 -&gt; 중지 버튼을 클릭
중지하면 과금도 중지되며, 1달 후에 자동으로 데이터베이스가 실행된다.</p>