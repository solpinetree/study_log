<h1 id="데이터베이스">데이터베이스</h1>
<h2 id="정의">정의</h2>
<h3 id="데이터베이스-1">데이터베이스</h3>
<p>여러 사람이 공유하여 사용할 목적으로 체계화해 통합, 관리하는 데이터의 집합체</p>
<h3 id="dbms">DBMS</h3>
<p>사용자와 데이터베이스 사이에서 사용자의 요구에 따라 정보를 생성해주고 데이터베이스를 관리해주는 소프트웨어</p>
<h3 id="관계형-데이터베이스">관계형 데이터베이스</h3>
<p>RDB : Relational Database
서로간에 관계가 있는 데이터 테이블을 모아둔 데이터 저장공간</p>
<h3 id="sql">SQL</h3>
<p>Structured Query Language
데이터베이스에서 데이터를 정의, 조작, 제어하기 위해 사용하는 언어</p>
<h4 id="구성">구성</h4>
<ul>
<li>데이터 정의 언어(DDL : Data Definition Language)
  CREATE, ALTER, DROP 등의 명령어</li>
<li>데이터 조작 언어(DML : Data Manipulation Language)
  INSERT, UPDATE, DELETE, SELECT 등의 명령어</li>
<li>데이터 제어 언어(DCL : Data Control Language)
  GRANT, REVOKE, COMMIT, ROLLBACK 등의 명령어</li>
</ul>
<blockquote>
<p>데이터 사이언티스트가 가장 많이 쓰는 명령어
:    <code>SELECT</code></p>
</blockquote>
<h2 id="관리">관리</h2>
<h3 id="데이터베이스-관리">데이터베이스 관리</h3>
<h4 id="create">CREATE</h4>
<pre><code class="language-sql">CREATE DATABASE dbname;</code></pre>
<blockquote>
<p>다국어와 이모지 문자 지원
CREATE DATABASE dbname DEFUALT CHARACTER SET utf8mb4;</p>
</blockquote>
<h4 id="drop">DROP</h4>
<pre><code class="language-sql">DROP DATABASE dbname;</code></pre>
<h3 id="user-관리">User 관리</h3>
<p>사용자 정보는 mysql database 에서 관리하므로 mysql database로 이동 후 조회</p>
<pre><code class="language-sql">USE mysql;
SELECT host, user FROM USER;</code></pre>
<h4 id="user-생성">User 생성</h4>
<ul>
<li><p>현재 PC에서만 접속 가능한 사용자를 비밀번호와 함께 생성(localhost)</p>
<pre><code class="language-sql">CREATE USER 'username'@'localhost' identified by 'password';</code></pre>
</li>
<li><p>외부에서 접속 가능한 사용자를 비밀번호와 함께 생성(%)</p>
<pre><code class="language-sql">CREATE USER 'username'@'%' identified by 'password';</code></pre>
</li>
</ul>
<h4 id="user-삭제">User 삭제</h4>
<p>host 정보가 다른 유저는 username이 같아도 됨.
따라서, 접근 범위에 따라 같은 이름의 사용자여도 별도로 삭제</p>
<pre><code class="language-sql">DROP USER 'username'@'localhost'
DROP USER 'username'@'%'</code></pre>
<h3 id="user-권한-관리">User 권한 관리</h3>
<h4 id="권한-확인">권한 확인</h4>
<pre><code class="language-sql">SHOW GRANTS FOR 'username'@'localhost';</code></pre>
<h4 id="권한-부여">권한 부여</h4>
<ul>
<li>사용자에게 특정 데이터베이스의 모든 권한을 부여<pre><code class="language-sql">GRANT ALL ON dbname.* to 'usernaem'@'localhost';</code></pre>
</li>
</ul>
<blockquote>
<p>수정내용이 적용이 되지 않는 경우 새로고침
FLUSH PRIVILEGES;</p>
</blockquote>
<h4 id="권한-제거">권한 제거</h4>
<ul>
<li>사용자에게 특정 데이터베이스의 모든 권한을 삭제<pre><code class="language-sql">REVOKE ALL ON dbname.* from 'username'@'localhost';</code></pre>
</li>
</ul>
<p><br /><br /></p>
<h1 id="table">Table</h1>
<h2 id="정의-1">정의</h2>
<p>데이터베이스 안에서 실제 데이터가 저장되는 형태이고, 행(Row)와 열(Column)로 구성된 데이터 모음</p>
<h2 id="생성">생성</h2>
<pre><code class="language-sql">CREATE TABLE tablename(
    columnname datatype,
    columnnae datatype,
    ...
);</code></pre>
<blockquote>
<p>예시</p>
</blockquote>
<pre><code class="language-sql">CREATE TABLE celeb(
    ID int NOT NULL AUTO_INCREMENT PRIMARY KEY,
    NAME varchar(32) NOT NULL DEFAULT ''
);</code></pre>
<h2 id="목록-확인">목록 확인</h2>
<pre><code class="language-sql">SHOW TABLES;</code></pre>
<h2 id="정보-확인">정보 확인</h2>
<pre><code class="language-sql">DESC tablename;</code></pre>
<h2 id="변경">변경</h2>
<h3 id="이름-변경">이름 변경</h3>
<pre><code class="language-sql">ALTER TABLE tablename 
RENAME new_tablename;</code></pre>
<h3 id="column-추가">column 추가</h3>
<pre><code class="language-sql">ALTER TABLE tablename
ADD COLUMN columnname datatype;</code></pre>
<h4 id="column-의-데이터타입-변경">column 의 데이터타입 변경</h4>
<pre><code class="language-sql">ALTER TABLE tablename
MODIFY COLUMN columnname datatype;</code></pre>
<h4 id="column의-이름-변경">column의 이름 변경</h4>
<pre><code class="language-sql">ALTER TABLE tablename
CHANGE COLUMN old_columnname new_columnname new_datatype;</code></pre>
<h4 id="column-삭제">column 삭제</h4>
<pre><code class="language-sql">ALTER TABLE tablename
DROP COLUMN columnname;</code></pre>
<h2 id="삭제">삭제</h2>
<pre><code class="language-sql">DROP TABLE tablename;</code></pre>
<h1 id="데이터-조작-언어dml">데이터 조작 언어(DML)</h1>
<p>SELECT, INSERT, UPDATE, DELETE</p>
<h2 id="insert">INSERT</h2>
<pre><code class="language-sql">INSERT INTO tablename (column1, column2, ...)
VALUES (value1, value2, ...)</code></pre>
<h3 id="모든-컬럼값을-추가하는-경우">모든 컬럼값을 추가하는 경우</h3>
<p>모든 컬럼값을 추가하는 경우에는 컬럼 이름을 지정하지 않아도 되지만,
입력하는 값의 순서가 테이블의 컬럼 순서와 일치하도록 주의</p>
<pre><code class="language-sql">INSERT INTO tablename
VALUES (value1, value2, ...)</code></pre>
<h2 id="select">SELECT</h2>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tablename;</code></pre>
<h3 id="where---조건">WHERE - 조건</h3>
<p>SQL 문에 조건을 추가하며 <code>SELECT</code> 뿐만 아니라 <code>UPDATE</code>와 <code>DELETE</code> 에도 사용</p>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tablename
WHERE condition;</code></pre>
<h2 id="update">UPDATE</h2>
<pre><code class="language-sql">UPDATE tablename
SET column1 = value1, column2 = value2
WHERE condition;</code></pre>
<h2 id="delete">DELETE</h2>
<pre><code class="language-sql">DELETE FROM tablename
WHERE condition;</code></pre>
<h1 id="order-by">ORDER BY</h1>
<p>SELECT 문에서 데이터를 특정 컬럼을 기준으로 오름차순 혹은 내림차순 정렬</p>
<ul>
<li>ASC(Ascending) : 오름차순으로 정렬</li>
<li>DESC(Descending) : 내림차순으로 정렬</li>
</ul>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tablename
ORDER BY column1, column2, ... ASC | DESC</code></pre>
<h2 id="여러-컬럼을-이용한-order-by">여러 컬럼을 이용한 ORDER BY</h2>
<h3 id="기본은-asc">기본은 ASC</h3>
<pre><code class="language-sql">SELECT age, name
FROM celeb
ORDER BY age, name;</code></pre>
<p>-&gt;나이로 먼저 정렬 후, 같은 나이일 경우 이름으로 정렬</p>
<h3 id="컬럼명-정렬-기준이-다를-경우">컬럼명 정렬 기준이 다를 경우</h3>
<pre><code class="language-sql">SELECT age, name
FROM celeb
ORDER BY age DESC, name ASC;</code></pre>
<h1 id="comparison-operators">Comparison Operators</h1>
<p><code>WHERE</code> 문에서 사용</p>
<h2 id="연산자">연산자</h2>
<p><code>A&lt;&gt;B</code> : A가 B보다 크거나 작은(같지 않은)</p>
<p><br /><br /></p>
<h1 id="logical-operations">Logical Operations</h1>
<p><code>WHERE</code> 문에서 사용</p>
<h2 id="연산자-1">연산자</h2>
<ul>
<li>AND</li>
<li>OR</li>
<li>NOT</li>
<li>BETWEEN : 조건값이 범위 사이에 있으면 TRUE</li>
<li>IN</li>
<li>LIKE : 조건값이 패턴에 맞으면 TRUE</li>
</ul>
<h2 id="and">AND</h2>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tablename
WHERE condition1 AND condition2 AND condition3 ...;</code></pre>
<h2 id="or">OR</h2>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tablename
WHERE condition1 OR condition2 OR condition3 ...;</code></pre>
<blockquote>
<p>AND가 OR 보다 우선순위가 높음(괄호로 연산을 묶어주는 것이 좋음)</p>
</blockquote>
<pre><code class="language-sql">SELECT * FROM celeb 
WHERE agency='YG엔터테인먼트' OR agency='나무엑터스'
AND age&lt;30;</code></pre>
<h2 id="not">NOT</h2>
<p>조건을 만족하지 않는 경우 TRUE</p>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tablename
WHERE NOT condition;</code></pre>
<h2 id="between">BETWEEN</h2>
<p>조건값이 범위 사이에 있으면 TRUE</p>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tablename
WHERE column1 BETWEEN value1 AND value2;</code></pre>
<blockquote>
<p>NOT과 BETWEEN 같이 사용하는 예시</p>
</blockquote>
<pre><code class="language-sql">SELECT * FROM celeb
WHERE agency='YG엔터테인먼트' AND
NOT age BETWEEN 20 AND 40;</code></pre>
<h2 id="in">IN</h2>
<p>목록 안에 조건이 존재하는 경우 TRUE</p>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tablename
WHERE column IN (value1, value2, ...);</code></pre>
<h2 id="like">LIKE</h2>
<p>조건값이 패턴에 맞으면 TRUE</p>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tablename
WHERE column LIKE pattern;</code></pre>
<h3 id="예제">예제</h3>
<ul>
<li><p>'YG'로 시작하는 소속사 이름을 가진 데이터 검색</p>
<pre><code class="language-sql">SELECT * 
FROM celeb
WHERE agency LIKE 'YG%';</code></pre>
</li>
<li><p>'엔터테인먼트'로 끝나는 소속사 이름을 가진 데이터 검색</p>
<pre><code class="language-sql">SELECT * 
FROM celeb
WHERE agency LIKE '%엔터테인먼트';</code></pre>
</li>
<li><p>직업명에 '가수'가 포함된 데이터 검색</p>
<pre><code class="language-sql">SELECT * 
FROM celeb
WHERE job_title LIKE '%가수%';</code></pre>
</li>
<li><p>소속사 이름의 두번째 글자가 G인 데이터 검색</p>
<pre><code class="language-sql">SELECT * 
FROM celeb
WHERE agency LIKE '_G%';</code></pre>
</li>
<li><p>직업명이 '가'로 시작하고 최소 2글자 이상인 데이터 검색</p>
<pre><code class="language-sql">SELECT * 
FROM celeb
WHERE agency LIKE '가_%';</code></pre>
</li>
<li><p>직업명이 '영'으로 시작하고 '모델'로 끝나는 데이터 검색</p>
<pre><code class="language-sql">SELECT * 
FROM celeb
WHERE job_title LIKE '영%모델';</code></pre>
</li>
<li><p>영화배우와 탤런트를 병행하는 데이터 검색</p>
<pre><code class="language-sql">SELECT * 
FROM celeb
WHERE job_title LIKE '%영화배우%' AND job_title LIKE '%탤런트%';</code></pre>
</li>
<li><p>직업이 하나 이상인 연예인 중 영화배우 혹은 탤런트가 아닌 연예인 검색</p>
<pre><code class="language-sql">SELECT * 
FROM celeb
WHERE job_title LIKE '%,%' AND NOT (job_title LIKE '%영화배우%'OR job_title LIKE '%탤런트%');</code></pre>
</li>
</ul>
<p><br /><br /></p>
<h1 id="union">Union</h1>
<p>여러개의 SQL문을 합쳐서 하나의 SQL 문으로 만들어주는 방법
(💡 컬럼의 개수가 같아야함)</p>
<h2 id="문법">문법</h2>
<pre><code class="language-sql">SELECT column1, column2, ... FROM tableA
UNION | UNION ALL
SELECT column1, column2, ... FROM tableB;</code></pre>
<h3 id="union-1">UNION</h3>
<p>중복된 값을 제거하여 알려준다.</p>
<h3 id="union-all">UNION ALL</h3>
<p>중복된 값도 모두 보여준다. </p>
<p><br /><br /></p>
<h1 id="join">JOIN</h1>
<p>두 개 이상의 테이블을 결합하는 것</p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/84b28750-9268-4b01-a27b-e5ce83d81bed/image.png" />
출처 : <a href="https://www.dofactory.com/sql/join">https://www.dofactory.com/sql/join</a></p>
<h2 id="inner-join">INNER JOIN</h2>
<p>두 개의 테이블에서 공통된 요소들을 통해 결합하는 조인 방식</p>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tableA
INNER JOIN tableB
ON tableA.column = tableB.column
WHERE condition;</code></pre>
<h3 id="예시">예시</h3>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/6eb98e50-0927-4715-8053-8bc7271c6eaa/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/20b62dd7-bd71-4ea3-a342-6fd041c9f2af/image.png" /></p>
<pre><code class="language-sql">SELECT celeb.id, celeb.name, snl_show.id,snl_show.host 
FROM celeb 
INNER JOIN snl_show 
ON celeb.name = snl_show.host;</code></pre>
<ul>
<li>결과
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/9bb6b671-122c-4c52-971d-b977b25a9326/image.png" /></li>
</ul>
<h2 id="left-join">LEFT JOIN</h2>
<p>두개의 테이블에서 공통영역을 포함해 왼쪽 테이블의 다른 데이터를 포함하는 조인 방식</p>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tableA
LEFT JOIN tableB
ON tableA.column = tableB.column
WHERE condition;</code></pre>
<h3 id="예시-1">예시</h3>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/6eb98e50-0927-4715-8053-8bc7271c6eaa/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/20b62dd7-bd71-4ea3-a342-6fd041c9f2af/image.png" /></p>
<pre><code class="language-sql">SELECT celeb.id, celeb.name, snl_show.id, snl_show.host 
FROM celeb 
LEFT JOIN snl_show 
ON celeb.name = snl_show.host;</code></pre>
<ul>
<li>결과
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/ef8c51c9-0106-485f-bfb4-1de6ffa413e2/image.png" /></li>
</ul>
<h2 id="right-join">RIGHT JOIN</h2>
<p>두개의 테이블에서 공통영역을 포함해 오른쪽 테이블의 다른 데이터를 포함하는 조인방식</p>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tableA
RIGHT JOIN tableB
ON tableA.column = tableB.column
WHERE condition;</code></pre>
<h3 id="예시-2">예시</h3>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/6eb98e50-0927-4715-8053-8bc7271c6eaa/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/20b62dd7-bd71-4ea3-a342-6fd041c9f2af/image.png" /></p>
<pre><code class="language-sql">SELECT celeb.id, celeb.name, snl_show.id, snl_show.host 
FROM celeb 
RIGHT JOIN snl_show 
ON celeb.name = snl_show.host;</code></pre>
<ul>
<li>결과
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/5df99d31-afc1-4bf1-8c13-7fb949a30c38/image.png" /></li>
</ul>
<h2 id="full-outer-join">FULL OUTER JOIN</h2>
<p>두개의 테이블에서 공통영역을 포함하여 양쪽 테이블의 다른영역을 모두 포함하는 조인방식</p>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tableA
FULL OUTER JOIN tableB
ON tableA.column = tableB.column
WHERE condition;</code></pre>
<h3 id="예시-3">예시</h3>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/6eb98e50-0927-4715-8053-8bc7271c6eaa/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/20b62dd7-bd71-4ea3-a342-6fd041c9f2af/image.png" /></p>
<pre><code class="language-sql">SELECT celeb.id, celeb.name, snl_show.id, snl_show.host 
FROM celeb 
FULL OUTER JOIN snl_show 
ON celeb.name = snl_show.host;</code></pre>
<ul>
<li>결과</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/43157eec-41cf-42e2-ab20-e0d13551fff0/image.png" /></p>
<blockquote>
<p>MySQL 에서는 <code>FULL OUTER JOIN</code> 을 지원하지 않음
다음과 같은 쿼리로 MySQL 에서 FULL OUTER JOIN 과 같은 조회 가능</p>
</blockquote>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tableA
LEFT JOIN tableB on tableA.colum = tableB.column
UNION
SELECT column1, column2, ...
FROM tableA
RIGHT JOIN tableB ON tableA.column = tableB.column
WHERE condition;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/97e1b780-6a64-428d-b3ab-bae8e38f9870/image.png" /></p>
<h2 id="self-join">SELF JOIN</h2>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tableA, tableB, ...
WHERE condition;</code></pre>
<h3 id="예시-4">예시</h3>
<h4 id="1">1</h4>
<ul>
<li>snl_show 에 호스트로 출연한 celeb 을 기준으로 celeb 테이블과 snl_show 테이블을 self join</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/6eb98e50-0927-4715-8053-8bc7271c6eaa/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/20b62dd7-bd71-4ea3-a342-6fd041c9f2af/image.png" /></p>
<pre><code class="language-sql">SELECT celeb.id, celeb.name, snl_show.id, snl_show.host 
FROM celeb, snl_show 
WHERE celeb.name = snl_show.host;</code></pre>
<ul>
<li>결과</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/a07333a2-16a2-49ec-92f3-ccd6b8cba22b/image.png" /></p>
<h4 id="2">2</h4>
<ul>
<li>celeb 테이블의 연예인 중, snl_show에 host로 출연했고 소속사가 안테나인 사람의 이름과 직업을 검색</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/6eb98e50-0927-4715-8053-8bc7271c6eaa/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/20b62dd7-bd71-4ea3-a342-6fd041c9f2af/image.png" /></p>
<pre><code class="language-sql">SELECT celeb.name, celeb.job_title  
FROM celeb, snl_show 
WHERE celeb.name = snl_show.host AND celeb.agency like '%안테나%';</code></pre>
<ul>
<li>결과</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/62d40914-8132-4dad-9197-a5683cc23763/image.png" /></p>
<h1 id="concat">CONCAT</h1>
<p>여러 문자열을 하나로 합치거나 연결</p>
<pre><code class="language-sql">SELECT CONCAT('string1', 'string2', ...);</code></pre>
<h2 id="예시-5">예시</h2>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/5d9aae52-8406-4b07-9c35-134993ca9116/image.png" /></p>
<h1 id="alias">ALIAS</h1>
<p>컬럼이나 테이블 이름에 별칭 생성</p>
<pre><code class="language-sql">SELECT column AS alias
FROM tablename;</code></pre>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tablename AS alias;</code></pre>
<ul>
<li><code>AS</code> 키워드는 생략이 가능</li>
</ul>
<h1 id="distinct">DISTINCT</h1>
<p>검색한 결과의 중복을 제거</p>
<pre><code class="language-sql">SELECT DISTINCT column1, column2, ...
FROM tablename;</code></pre>
<h2 id="예시-6">예시</h2>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/c82110f5-848e-4181-b853-f6babaf3cab6/image.png" /></p>
<h1 id="limit">LIMIT</h1>
<p>검색결과를 정렬된 순으로 주어진 숫자만큼만 조회</p>
<pre><code class="language-sql">SELECT column1, column2, ...
FROM tablename
WHERE condition
LIMIT number;</code></pre>