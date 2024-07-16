<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/80e20902-b01a-4eb0-89b7-c8e37f9d7c57/image.png" />
matplotlib 의 기본 설정이 한글을 지원하지 않기 때문에 한글이 깨져서나온다.</p>
<h2 id="mac을-위한-해결책">mac을 위한 해결책</h2>
<p><img alt="" src="https://velog.velcdn.com/images/solpinetree/post/d9cda8a4-c097-4bf0-9ba6-6d0a96afebf1/image.png" />
이 코드를 실행하면 'Arial Unicode MS' 결과값이 나오는데 이 결과값을 다음 코드에서 사용한다.
<img alt="" src="https://velog.velcdn.com/images/solpinetree/post/1d98d549-a92a-42aa-99b5-7bd7886420f3/image.png" /></p>
<p>다시 에러났던 코드를 실행하면 한글이 안 깨져서 나온다. </p>
<h2 id="전체코드">전체코드</h2>
<pre><code class="language-python">from matplotlib import font_manager
from matplotlib import rc

f_path = &quot;/Library/Fonts/Arial Unicode.ttf&quot;
family = font_manager.FontProperties(fname=f_path).get_name()
rc(&quot;font&quot;, family=family)</code></pre>
<p>이를 매번 코드 위에서 실행시켜줘야한다.
<br />
<br />
<br /></p>
<blockquote>
<p>이 글은 제로베이스 데이터 취업 스쿨의 강의 자료 일부를 발췌하여 작성되었습니다.</p>
</blockquote>