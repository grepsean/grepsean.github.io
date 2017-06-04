{% include toc %}

# Jekyll 시작하기


- ## ruby 버전 업데이트
  Jekyll에서 필요로하는 ruby 버전과 현재 설치된 ruby버전이 다를 수 있으니, 되도록 업데이트 하는 것이 좋다.
  1. `$ brew update`
  2. `rvm` 설치하기
      - `\curl -sSL https://get.rvm.io | bash -s stable --ruby`
  3. rvm을 이요한 ruby 업데이트
      - `rvm list known` : 가용한 ruby 버전 확인
      - `rvm install ruby-2.4.0` : 해당 버전중 하나 설치
  4. 설치한 ruby 사용하기
      - `rvm user ruby-2.4.0`
      - `rvm user ruby-2.4.0 --default` : 해당 ruby 버전을 기본으로 사용 설정


- ## 필요한 패키지 설치
  1. `sudo gem install bundler`
  2. `sudo gem install jekyll`


- ## Jekyll(블로그) 생성하기
  1. `jekyll new myblog`
  2. `bundle install` : 생성된 디렉토리에서 dependencies 설치


- ## Jekyll(블로그) 실행하기 (Local에서 확인)
  1. `jekyll serve --watch` : local에서 jekyll 실행하기 (`--watch` 옵션은 변경시 자동 로딩을 위함)
  2. [http://localhost:4000](http://localhost:4000){:target="_blank"} 으로 접속해서 확인한다.


- ## GitHub Pages Dependencies 설치
  1. GitHub Pages에서 추가해야하는 Plugins
  ```
  gems:
   - jekyll-mentions
   - jemoji
   - jekyll-redirect-from
   - jekyll-sitemap
   - jekyll-feed
  ```
  2. (.gemspec 파일에) 아래를 적절히 추가한다.
  ```
  spec.add_runtime_dependency "jekyll-mentions", "~> 1.2.0"
  spec.add_runtime_dependency "jekyll-redirect-from", "~> 0.12.1"
  ```
