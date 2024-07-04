# apt-get

* apt-get은 인덱스를 가지고 있는데 이 인덱스는 /etc/apt/sources.list에 있습니다.&#x20;
* apt를 이용해서 설치된 deb패키지는 /var/cache/apt/archive/ 에 설치가 됩니다.

<table><thead><tr><th width="277">동작</th><th>command</th></tr></thead><tbody><tr><td>인덱스 정보를 업데이트</td><td><pre><code>sudo apt-get update
</code></pre></td></tr><tr><td>설치된 패키지 업그래이드</td><td><pre><code>sudo apt-get upgrade
</code></pre></td></tr><tr><td>설치된 패키지 리스트</td><td><pre><code>sudo apt-mark showmanual # 설치 지시한것
sudo apt-mark showauto   # 자동 설치한것
dpkg -l
</code></pre></td></tr><tr><td>패키지 리스트</td><td><pre><code>sudo apt-cache pkgnames
</code></pre></td></tr><tr><td>패키지 검색</td><td><pre><code>sudo apt-cache search &#x3C;패키지이름>
</code></pre></td></tr><tr><td>패키지 정보 보기</td><td><pre><code>sudo apt-cache show &#x3C;패키지이름>
</code></pre></td></tr><tr><td>의존성검사하며 설치하기</td><td><pre><code>sudo apt-get dist-upgrade
</code></pre></td></tr><tr><td>패키지 설치</td><td><pre><code>sudo apt-get install &#x3C;패키지이름>
</code></pre></td></tr><tr><td>패키지 재설치</td><td><pre><code>apt-get --reinstall install &#x3C;패키지이름>
</code></pre></td></tr><tr><td>패키지 삭제 <br>( 설정파일은 지우지 않음 )</td><td><pre><code>sudo apt-get remove &#x3C;패키지이름>
</code></pre></td></tr><tr><td>패키지 삭제</td><td><pre><code>sudo apt-get --purge remove &#x3C;패키지이름>
</code></pre></td></tr><tr><td>패키지 소스코드 다운로드</td><td><pre><code>sudo apt-get source &#x3C;패키지이름>
</code></pre></td></tr><tr><td>소스코드를 의존성있게 빌드</td><td><pre><code>sudo apt-get build-dep &#x3C;패키지이름>
</code></pre></td></tr><tr><td>패키지 버전 홀드</td><td><pre><code>sudo apt-mark hold &#x3C;패키지이름>
</code></pre></td></tr><tr><td>패키지 버전 홀드 제거</td><td><pre><code>sudo apt-mark unhole &#x3C;패키지이름>
</code></pre></td></tr><tr><td>홀드된 패키지 보기</td><td><pre><code>sudo apt-mark showhold
</code></pre></td></tr></tbody></table>
