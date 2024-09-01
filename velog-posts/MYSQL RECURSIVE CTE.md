<blockquote>
<p>CTE
Common Table Expression = WITH</p>
</blockquote>
<ul>
<li>MySQL 8.0 부터 재귀 CTE 를 지원</li>
<li>트리 구조나 계층적 데이터를 다룰 때 매우 유용</li>
</ul>
<h1 id="recursive-cte">Recursive CTE</h1>
<p>하나의 CTE(WITH절)가 자신을 재귀적으로 참조함으로써 트리 구조의 데이터나 계층형 데이터를 반복적으로탐색할 수 있게 해줌. </p>
<h2 id="구조">구조</h2>
<ul>
<li>처음 row</li>
<li>반복될 row</li>
</ul>
<pre><code class="language-sql">WITH RECURSIVE cte_name AS (
    -- 처음 row
    initial_query
    UNION ALL
    -- 재귀 row
    recursive_query
)
SELECT * FROM cte_name;</code></pre>
<p><code>UNION ALL</code> 대신 <code>UNION</code> 을 사용할 수도 있지만, <code>UNION</code> 은 중복된 결과를 제거하므로 재귀 쿼리에서는 주로 <code>UNION ALL</code>을 사용</p>
<p><br /><br /></p>
<h2 id="예제">예제</h2>
<p>프로그래머스의 &quot;멸종위기의 대장균 찾기&quot; SQL 문제에서 recursive query를 사용</p>
<h3 id="문제">문제</h3>
<h4 id="설명">설명</h4>
<p>대장균들은 일정 주기로 분화하며, 분화를 시작한 개체를 부모 개체, 분화가 되어 나온 개체를 자식 개체라고 합니다.
다음은 실험실에서 배양한 대장균들의 정보를 담은 <code>ECOLI_DATA</code> 테이블입니다. <code>ECOLI_DATA</code> 테이블의 구조는 다음과 같으며, <code>ID</code>, <code>PARENT_ID</code>, <code>SIZE_OF_COLONY</code>, <code>DIFFERENTIATION_DATE</code>, <code>GENOTYPE</code> 은 각각 대장균 개체의 ID, 부모 개체의 ID, 개체의 크기, 분화되어 나온 날짜, 개체의 형질을 나타냅니다.</p>
<table>
<thead>
<tr>
<th>컬럼</th>
<th>타입</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>ID</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>PARENT_ID</td>
<td>INTEGER</td>
<td>TRUE</td>
</tr>
<tr>
<td>SIZE_OF_COLONY</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>DIFFERENTIATION_DATE</td>
<td>DATE</td>
<td>FALSE</td>
</tr>
<tr>
<td>GENOTYPE</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
</tbody></table>
<ul>
<li>최초의 대장균 개체의 <code>PARENT_ID</code> 는 NULL</li>
</ul>
<h4 id="문제-1">문제</h4>
<ul>
<li>각 세대별 자식이 없는 개체의 수와 세대 조회</li>
<li>세대에 대해 오름차순 정렬</li>
</ul>
<p>-&gt; 이 문제의 키 포인트는 각 행의 세대를 알아내는 것
세대만 알아내면 문제에서 원하는 조회는 쉽다.</p>
<h3 id="recursive-사용해서-세대-알아내기">RECURSIVE 사용해서 세대 알아내기</h3>
<ol>
<li><code>GENERATION</code> COLUMN 추가</li>
<li>PARENT_ID = NULL 인 행 조회(예를 들어 ID = x)</li>
<li>ID = x 행의 <code>GENERATION</code> COLUMN 에 1 입력(1세대)</li>
<li>PARENT_ID = x 인 행을 찾아 <code>GENERATION</code> COLUMN 에 2 입력</li>
</ol>
<p>이런식으로 n번 반복</p>
<h4 id="with-절-정의">WITH 절 정의</h4>
<pre><code class="language-sql">WITH RECURSIVE CTE AS(
--- 여기에 처음 row 추가
UNION ALL
--- 반복문 돌릴 row 추가
)</code></pre>
<h4 id="처음-row">처음 row</h4>
<p>PARENT_ID = NULL 인 행들의 <code>GENERATION</code> 에 1을 입력한다. 
WITH 절을 이용한 조회(SELECT)로 RECURSIVE 의 결과인 TABLE 을 만드는 것</p>
<pre><code class="language-sql">SELECT ID, 1 AS GENERATION, PARENT_ID
FROM ECOLI_DATA WHERE PARENT_ID IS NULL</code></pre>
<p>-&gt; 이렇게 하면 CTE에 최초의 대장균 개체의 ID, PARENT_ID들이 저장되고 GENERATION 값이 1로 저장된다.</p>
<h4 id="반복될-row">반복될 row</h4>
<pre><code class="language-sql">SELECT e.ID, c.GENERATION + 1, e.PARENT_ID
FROM ECOLI_DATA e
INNER JOIN CTE c
ON e.PARENT_ID = c.ID</code></pre>
<p>처음 iteration 시에는 CTE에 최초의 대장균 개체의 row 들이 있으니까 INNER JOIN 해서 자식 개체를 찾아 GENERATION을 2로 설정한다. 
그 이후로는 이전의 iteration 때, CTE에 추가된 행들로만 INNER JOIN 을 하고, CTE에 추가되는 행이 없을 때까지 반복문이 돈다. </p>
<p>처음에는 반복문에서 CTE에 있는 모든 행들에 INNER JOIN을  하는데 왜 중복되는 값이 없나 헷갈렸는데, <strong>이전 iteration 에서 CTE에 추가된 행들</strong>하고만 INNER JOIN을 한다는 점을 알아야한다. </p>
<blockquote>
<p>이전 iteration 에서 CTE에 추가된 행들만 이번 iteration 에서 사용 </p>
</blockquote>
<pre><code class="language-sql">WITH RECURSIVE CTE AS(
    SELECT ID, 1 AS GENERATION, PARENT_ID
    FROM ECOLI_DATA WHERE PARENT_ID IS NULL
    UNION ALL
    SELECT 1, GENERATION + 1, 1
    FROM CTE e
    WHERE GENERATION &lt; 10
)</code></pre>
<p>이 sql 결과를 봤더니
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/2d87bbf4-c269-4bff-ac9e-48c3f3cbace3/image.png" />
각 GENERATION 마다 2개의 행이 있는 걸로 보아 이전 iteration 에서 추가된 행들만 CTE로 참조한다는 것을 알 수 있었다.</p>
<p><a href="https://stackoverflow.com/questions/55947537/recursive-cte-concept-confusion">참고</a></p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">WITH RECURSIVE CTE AS(
    SELECT ID, 1 AS GENERATION, PARENT_ID
    FROM ECOLI_DATA WHERE PARENT_ID IS NULL
    UNION ALL
    SELECT e.ID, c.GENERATION + 1, e.PARENT_ID
    FROM ECOLI_DATA e
    INNER JOIN CTE c
    ON e.PARENT_ID = c.ID
)


SELECT COUNT(*) AS COUNT, GENERATION FROM CTE c
WHERE (SELECT COUNT(*) FROM CTE WHERE PARENT_ID = c.ID) = 0
GROUP BY GENERATION
ORDER BY GENERATION</code></pre>
<p><a href="https://school.programmers.co.kr/learn/courses/30/lessons/301651">프로그래머스 - 멸종위기의 대장균 찾기</a></p>