<h2 id="environment-management">Environment Management</h2>
<p>이 환경에서만 사용되는 라이브러리와 파이썬 버전을 가지는 독립된 워크스페이스</p>
<h2 id="conda-env">conda env</h2>
<p>conda 는 오픈소스 패키지 관리 시스템.
conda로 여러 패키지를 설치할 수 있고, conda env 는 그 중 하나이다.
conda env 의 단순함과 복잡한 의존성을 관리하기 위해 데이터 사이언스에서 넓게 사용된다. </p>
<h2 id="venv">venv</h2>
<p>python 3.3 포함 이후의 python 과 함께 제공되는 모듈이다. 이는 virtual environments를 생성한다. 가볍고, 따로 설치가 불필요하며 단순 파이썬 프로젝트에는 훌륭하다.</p>
<h2 id="pyenv">pyenv</h2>
<p>package manager는 아니다. 이건 파이썬 버전을 변경하기 쉽게 해준다. 다른 프로젝트들이 서로 다른 파이썬 버전으로 개발될 때 유용하다.</p>
<h2 id="virtualenv">virtualenv</h2>
<p>독립된 파이썬 환경을 만드는 데에 유명하다. python2 를 포함한 어느 버전의 파이썬으로 환경을 만들 수 있어 venv보다 유연하다. </p>
<h2 id="비교">비교</h2>
<h3 id="사용하기-쉬운-것">사용하기 쉬운 것</h3>
<p>conda, venv 는 사용하기 단순하기 때문에 가장 사용하기 쉽다. </p>
<h3 id="유연성">유연성</h3>
<p>pyenv, virtualenv 는 파이썬 버전에 제약이 없기에 conda, venv 로 사용 못하는 파이썬 버전 프로젝트의 경우 pyenv, virtualenv 를 사용하는 게 좋을 것 같다.</p>
<p>출처
<a href="https://saturncloud.io/blog/understanding-python-environment-management-conda-env-vs-venv-pyenv-virtualenv/">https://saturncloud.io/blog/understanding-python-environment-management-conda-env-vs-venv-pyenv-virtualenv/</a></p>