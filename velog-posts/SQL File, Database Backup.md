<blockquote>
<p>💡 <strong>SQL File 이란</strong>
SQL 쿼리를 모아놓은 파일</p>
</blockquote>
<h1 id="sql-file-실행">SQL File 실행</h1>
<h2 id="로그인-이후">로그인 이후</h2>
<pre><code class="language-sql">source &lt;/path/filename.sql&gt;</code></pre>
<ul>
<li><p>source 대신 <code>\.</code> 사용 가능</p>
<pre><code class="language-sql">\. &lt;/path/filename.sql&gt;</code></pre>
</li>
<li><p>현재 폴더에 파일이 있으면 path 생략 가능</p>
<pre><code class="language-sql">\. &lt;filename.sql&gt;</code></pre>
</li>
</ul>
<h2 id="외부에서-바로-실행">외부에서 바로 실행</h2>
<pre><code class="language-bash">mysql -u username -p &lt;database&gt; &lt; &lt;/path/filename.sql&gt;</code></pre>
<p><br /><br /></p>
<h1 id="database-backup">Database Backup</h1>
<h2 id="sql-file로-database-백업">SQL File로 Database 백업</h2>
<h3 id="특정-database-백업">특정 Database 백업</h3>
<pre><code class="language-sql">mysqldump -u username -p dbname &gt; backup.sql</code></pre>
<h3 id="모든-database-백업">모든 Database 백업</h3>
<pre><code class="language-sql">mysqldump -u username -p --all-databases &gt; bakcup.sql</code></pre>
<br />

<h1 id="database-restore">Database Restore</h1>
<p>백업한 SQL File 을 실행한다</p>
<br />

<h1 id="table-backup">Table Backup</h1>
<p>테이블 단위로도 백업을 할 수 있다.</p>
<pre><code class="language-sql">mysqldump -u username -p dbname tablename &gt; backup.sql</code></pre>
<br />

<h1 id="table-restore">Table Restore</h1>
<p>Table을 백업한 SQL File 을 실행하여, 해당 테이블을 복구하거나 이전할 수 있다. </p>
<br />

<h1 id="table-schema-backup">Table Schema Backup</h1>
<p>데이터를 제외하고 테이블 생성 쿼리만 백업할 수 있다. (Table Backup 명령어에 <code>-u</code> 옵션을 추가하면 된다.)</p>
<h2 id="특정-table-schema-backup">특정 Table Schema Backup</h2>
<pre><code class="language-sql">mysqldump -d -u username -p dbname tablename &gt; backup.sql</code></pre>
<h2 id="모든-table-schema-backup">모든 Table Schema Backup</h2>
<pre><code class="language-sql">mysqldump -d -u username -p dbname &gt; backup.sql</code></pre>
<br />

<h1 id="aws-rds-에서-sql-백업">AWS RDS 에서 SQL 백업</h1>
<blockquote>
<p>💡 <strong>--set-gtid-purged=OFF 옵션을 추가해야함</strong>
AWS의 AWS 는 GTID 를 사용하는데, 보통의 MysqlDB Restorersms GTID를 사용하지 않기 때문
(출처 : <a href="https://iizz.tistory.com/m/339">https://iizz.tistory.com/m/339</a>)</p>
</blockquote>
<pre><code class="language-bash">mysqldump --set-gtid-purged=OFF -h &lt;host&gt; -P &lt;port&gt; -u admin -p 
&lt;dbname&gt; &gt; aws_zerobase.sql</code></pre>