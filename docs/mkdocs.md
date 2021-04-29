# Welcome to MkDocs
<br>
For full documentation visit [mkdocs.org](https://www.mkdocs.org).
<br>
<br>
<br>
## Mkdocs Install/Update
<br>
 python installer

   - 파이썬 설치 및 버전확인
     - `python --verion`
     - `pip --version`
 <br>
 Mkdocs install

   - pip 업그레이드
     - `pip install --upgrade pip`
   - mkdocs 설치
     - `pip install mkdocs`
   - 버전확인
     - `mkdocs --version`

<br>
## Commands
<br>

 * `mkdocs new [dir-name]` - mkdocs 폴더를 생성한다.
 * `mkdocs serve` - mkdocs 개발 서버를 실행한다. http://localhost:8000
 * `mkdocs build` - mkdocs site를 빌드해준다.
 * `mkdocs -h` - 도움말 정보가 보여진다.

<br>
<br>

## Project layout
<br>

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

<br>

## Adding Pages

<br>

mkdocs.yml 파일에 `nav` 세팅을 추가해서 navigation header를 추가 할 수 있다.
  
  ```
  site_name: MkLorum
  nav:
    - Home: index.md
    - About: about.md
  ```

<br>

## Site Building

<br>

`mkdocs build --clean` 시에 site 폴더가 생성된다. 해당 폴더 구성은 다음과 같다.

    $ ls site
    about  fonts  index.html  license  search.html
    css    img    js          mkdocs   sitemap.xml

<br>

## Site Deploying

<br>

`mkdocs gh-deploy` 사용하고 github 저장소에 올리면 `https://아이디.github.io/저장소이름`으로 문서 접근이 가능하다. ex) `https://joy2734.github.io/wiki`

<br>
<br>
<br>
<br>
<br>