# Welcome to MkDocs

For full documentation visit [mkdocs.org](https://www.mkdocs.org).


## Mkdocs Install/Update

 python installer

   - 파이썬 설치 및 버전확인
     - `python --verion`
     - `pip --version`
 
 Mkdocs install

   - pip 업그레이드
     - `pip install --upgrade pip`
   - mkdocs 설치
     - `pip install mkdocs`
   - 버전확인
     - `mkdocs --version`



## Commands
 
 * `mkdocs new [dir-name]` - mkdocs 폴더를 생성한다.
 * `mkdocs serve` - mkdocs 개발 서버를 실행한다. http://localhost:8000
 * `mkdocs build` - mkdocs site를 빌드해준다.
 * `mkdocs -h` - 도움말 정보가 보여진다.


## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.


## Adding Pages

mkdocs.yml 파일에 `nav` 세팅을 추가해서 navigation header를 추가 할 수 있다.
  
  ```
  site_name: MkLorum
  nav:
    - Home: index.md
    - About: about.md
  ```

## Site Building

`mkdocs build` 시에 site 폴더가 생성된다. 해당 폴더 구성은 다음과 같다.

    $ ls site
    about  fonts  index.html  license  search.html
    css    img    js          mkdocs   sitemap.xml