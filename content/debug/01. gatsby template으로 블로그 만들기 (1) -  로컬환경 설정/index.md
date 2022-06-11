---
emoji: 🛠
title: gatsby template으로 블로그 만들기(1) - 로컬환경 설정
date: '2022-05-31 23:00:00'
author: hwan
tags: blog gatsby 개츠비 블로그
categories: Debug
---

#### 목차
 1. 로컬 환경 만들기
 2. 나의 삽질기

</br>
</br>

## 1. 로컬 환경 만들기  

---

**1.1  node, npm, gatsby 설치하기**

gatsby는 react.js 기반으로 node를 설치해야한다.  
npm은 자바스크립트의 패키지 관리자로 대신 yarn을 사용할 수도 있다.  

</br>

- homebrew로 node.js설치 <sup>[1](#footnote_1)</sup>
    - `brew install node@16` 
    - node 16 버전으로 설치하기
    - node 18 버전에서 gatsby build error 발생하기 때문 

- homebrew로 npm 설치하기
    - `brew install npm`
    - Q. npm이 뭐하는거지? -> [(참고: npm등 패키지 관리자 설명 포스트)](https://yceffort.kr/2022/05/npm-vs-yarn-vs-pnpm)  

- gatsby 설치하기
    - `brew install g gatsby-cli`

</br>

``` 
brew install node@16  # node 16 설치
brew install npm  # npm 설치
npm install -g gatsby-cli  # gatsby 설치

#brew install node #가장 최신의 node로 설치됨
```
</br>
</br>

**1.2  잘 설치되었는지 버전 확인하기**


```
node -v  # node 버전확인 >> v16.15.0
npm -v  # npm 버전확인 >> 8.10.0
gatsby -v  # gatsby 버전확인 >> Gatsby CLI version: 4.14.0

```
</br>
</br>

**1.3  선택한 템플릿을 내가 작업할 디렉토리에 클론하기**

- `gatsby new [dir name] [gatsby address]`  

- 나의 경우 줌코딩 님의 템플릿을 사용하였다.
    - 줌코딩 님 gatsby 템플릿 : [링크](https://github.com/zoomkoding/zoomkoding-gatsby-blog)

</br>

```
# gatsby new hwnm-study <https://github.com/zoomkoding/zoomkoding-gatsby-blog>

```
</br>
</br>

**1.4  해당 디렉토리에서 개츠비 실행하기**


- 해당 디렉토리로 이동하기
    - `cd [dir name]`

- 개츠비 실행하기
    - `npm install`
    - `gatsby develop`

- 잘 실행되었는지 로컬 환경에서 확인하기
    - localhost:8000

</br>

```
# cd hwnm-study

npm install
gatsby develop

```
</br>
</br>

**1.5  (번외) 줌코딩님의 템플릿 디벨롭시 마주하는 에러**


- `gatsby develop`  후 JavaScript bundle failed 에러 발생 시
    - node 버전 확인하기
    - 18버전이라면 16으로 다운그레이드해주기

- `npm install` 후 버전의 문제로 dependency 에러 발생 시
    - `rm package-lock.json` : package-lock.json 삭제하기
    - `rm -rf node_modeules` : node_modules 폴더 삭제하기
    - `npm install --legacy-peer-deps` : dependency 무시하고 실행하기

- `gatsby develop`  후 Module not found 에러 발생 시
    - `npm install @emotion/react`, `npm install @emotion/styled` : 부족한 모듈 따로 설치하기

- 위 과정 후 `gatsby develop`  이 여전히 실행되지 않는다면 `gatsby clean`로 캐시를 삭제해주자

</br>
</br>
</br>
</br>

## 🛠 2. 나의 삽질기
---

> 
> - 기록이유. 위의 번외에서 에러별 해결방법을 적어놨으나 앞으로 더 효율적인 디버깅을 위하여 이번 나의 디버깅 과정을 순차적으로 기록해둔다. 누군가에겐 몇 분이면 끝날 과정이겠지만 나에겐 아니었다. 더 많이 마주치면서 효율적으로 적은 시간안에 해결할 수 있기를.
> - **배움1. 공식 문서를 참고하자!**  
>    gatsby 공식 홈페이지에 troubleshooting common error 문서에 내가 마주한 몇 에러들이 있었다. (모듈 설치, 캐시 삭제)
> - **배움2. 버전을 잘 확인하자!**
> - **배움3. 에러메세지를 잘 확인하자!**  
>    키워드를 잘 찾으면 stackoverflow에 해당 이슈를 마주치고 해결한 결과가 있다.

</br>
</br>

### 2.1 dependency 에러

node와 npm, gatsby가 잘 설치되었다. (라고 생각한 여기가 문제였다..)  
gatsby를 실행할 디렉토리를 생성해주고 해당 템플릿을 실행하기 위해 가져오는 과정에서 에러가 발생했다.  

```
gatsby new study <https://github.com/zoomkoding/zoomkoding-gatsby-blog>

```


에러를 무시하고 생성된 node_modules폴더와 package-lock파일(해당 템플릿에서 써야하는 패키지가 package.json에 적혀 있는 데 그것과 관련하여 잘못된 부분)을 삭제하고 npm install, npm start를 강행했지만 역시나 계속해서 실행이 불가하였다.

```
npm cache clean --force
rm -rf node_modules
rm package-lock.json

```
내가 받은 첫번째 에러코드는 아래와 같다.   
버전호환문제인 dependency 에러였다.  

```
#첫 에러코드

npm  ERR!  code ERESOLVE
npm  ERR!  ERESOLVE could not resolve
npm  ERR!
npm  ERR! While resolving: gatsby-plugin-advanced-sitemap@2.0.0
npm  ERR! Found: gatsby@4.9.3
npm  ERR!  node_modules/gatsby
npm  ERR!  gatsby@"^4.9.3" from the root project
npm  ERR!  peer  gatsby@"^4.0.0-next" from babel-plugin-remove-graphql-queries@4.9.1
npm  ERR!  node_modules/babel-plugin-remove-graphql-queries
npm  ERR!  babel-plugin-remove-graphql-queries@"^4.9.1" from gatsby@4.9.3
npm  ERR!  babel-plugin-remove-graphql-queries@"^4.9.1" from gatsby-plugin-image@2.9.1
npm  ERR!  node_modules/gatsby-plugin-image
npm  ERR!  gatsby-plugin-image@"^2.9.1" from the root project
npm  ERR! 1 more (gatsby-plugin-typescript)
npm  ERR! 26 more (gatsby-material-ui-components, ...)
npm  ERR!
npm  ERR! Could not resolve dependency:
npm  ERR!  peer  gatsby@"^3.0.0" from gatsby-plugin-advanced-sitemap@2.0.0
npm  ERR!  node_modules/gatsby-plugin-advanced-sitemap
npm  ERR!  gatsby-plugin-advanced-sitemap@"^2.0.0" from the root project
npm  ERR!
npm  ERR! Conflicting peer dependency: gatsby@3.14.6
npm  ERR!  node_modules/gatsby
npm  ERR!  peer  gatsby@"^3.0.0" from gatsby-plugin-advanced-sitemap@2.0.0
npm  ERR!  node_modules/gatsby-plugin-advanced-sitemap
npm  ERR!  gatsby-plugin-advanced-sitemap@"^2.0.0" from the root project
npm  ERR!
npm  ERR! Fix the upstream dependency conflict, or retry
npm  ERR! this command with --force, or --legacy-peer-deps
npm  ERR! to accept an incorrect (and potentially broken) dependency resolution.
npm  ERR!
npm  ERR! See /Users/hwanimchu93/.npm/eresolve-report.txt for a full report.
npm  ERR! A complete log of this run can be found in:

ERROR
Command failed with exit code 1: npm install

Error: Command failed with exit code 1: npm install
-  error.js:60 makeError
[lib]/[gatsby-cli]/[execa]/lib/error.js:60:11
-  index.js:118 handlePromise
[lib]/[gatsby-cli]/[execa]/index.js:118:26
-  task_queues:95 processTicksAndRejections
node:internal/process/task_queues:95:5
-  init-starter.js:135 install
[lib]/[gatsby-cli]/lib/init-starter.js:135:7
-  init-starter.js:202 clone
[lib]/[gatsby-cli]/lib/init-starter.js:202:3
-  init-starter.js:343 initStarter
[lib]/[gatsby-cli]/lib/init-starter.js:343:5
-  create-cli.js:460
[lib]/[gatsby-cli]/lib/create-cli.js:460:9

```

</br>
</br>

### 2.2 내 로컬의 문제? 아니면 gatsby 템플릿의 문제?

내가 사용하려던 템플렛의 문제인지 gatsby자체를 돌리지 못하는 것인지 확인하기 위해  
gatsby 공식 홈페이지에서 제공하는 템플릿을 로컬에서 시도해보기로 했다.

> [ 버전 확인 ]  
> node -v    : v18.2.0  
> npm -v    : 8.10.0  
> gatsby -v     : Gatsby CLI version: 4.14.0  
>   
</br>


```
#다른 템플릿 로컬에 클론
gatsby new gatsby-casper <https://github.com/scttcper/gatsby-casper>

```
</br>


dependency관련 문제가 있지만 에러가 아니라 경고이고,  
gatsby사이트를 디벨롭하는데 성공했다.

```
#경고
npm  WARN  ERESOLVE overriding peer dependency
.
.

#디벨롭 성공
Your new Gatsby site has been successfully bootstrapped. Start developing it by running:

cd gatsby-casper
gatsby develop

```
</br>

localhost:8000으로 접속하여 화면이 잘 나오는 것을 확인.  
이로써 내 로컬환경에서 gatsby를 돌리는 데 문제가 없다는 것을 확인했다.  
다시 zoomkoding님의 템플릿을 실행하기 위해 디버깅을 해보자.

</br>
</br>


### 2.3 zoomkoding 템플릿 다시 시도

</br>

**2.3.1 줌코딩 템플릿 클론 후 npm install**  

: 디벨롭 할 수 없다
    
    
    gatsby new study <https://github.com/zoomkoding/zoomkoding-gatsby-blog>
    
    cd study  # 해당 디렉토리로 이동
    gatsby develop
    >> ERROR
    >> There was a problem loading the local develop command. Gatsby may not be installed in your site's "node_modules" directory.
    >> Perhaps you need to run "npm install"? You might need to delete your "package-lock.json" as well.
    
    rm package-lock.json  # 에러에서 말한대로 삭제
    rm -rf node_modeules  # 제대로 설치되지 않았으므로 삭제
    
    npm install
    >> WARN
    >> Some issues need review, and may require choosing
    
    gatsby develop
    >> ERROR
    >> Generating development JavaScript bundle failed
    
    
</br>
</br>
    
**2.3.2. 패키지 실행 시 dependency 무시하고 진행하기** 

- ```npm install --legacy-peer-deps```  
    - dependency 무시하고 진행하기
    - [(참고: npm install `-force` and `-legacy-peer-deps` 차이점)](https://velog.io/@yonyas/Fix-the-upstream-dependency-conflict-installing-NPM-packages-%EC%97%90%EB%9F%AC-%ED%95%B4%EA%B2%B0%EA%B8%B0)  


- `npm install @emotion/react`, `npm install @emotion/styled` 
    - 디벨롭 시 모듈이 없음, 그 모듈 따로 설치


: 하지만 여전히 디벨롭 할 수 없다.


    
    
    rm package-lock.json && rm -rf node_modeules  # 윗 단계에서 gatsby develop하면서 또 생성됐으므로 다시 삭제
    
    npm install --legacy-peer-deps  # dependency 무시하고 진행
    >> WARN
    >> Some issues need review, and may require choosing a different dependency.
    
    gatsby develop
    >> ERROR
    >> Module not found: Error: Can't resolve '@emotion/react'
    >> Module not found: Error: Can't resolve '@emotion/styled'
    
    npm install @emotion/react # 모듈 따로 설치
    npm install @emotion/styled
    
    gatsby develop
    >> ERROR
    >> Generating development JavaScript bundle failed
    
    
</br>
</br>
    


**2.3.3. node 버전 바꾸기**

: 노드 버전 16으로 바꾼후 디벨롭 성공
    
 이 템플릿을 사용한 후기도 찾아 보면서 앞에까지의 디버깅이 비슷한데 왜 내 로컬에선 안될까 생각하다가..  
 여기서 부터 노드버전의 문제라는 것을 깨달았다.
    
    gatsby develop
    >> ERROR: Generating development JavaScript bundle failed

</br>
    
위 에러로 검색하니 노드 18로 개츠비를 사용하다가 해당 이슈에 직면한 케이스가 있었다.  
- [(참조: stackoverflow -  gatsby build error webpack related maybe)](https://stackoverflow.com/questions/71991480/gatsby-build-error-webpack-related-maybe)
    
맨 처음 에러 후, 문제가 로컬인지 템플릿인지 확인할 때 gatsby-casper 템플릿 실행시 받았던 경고에서도 (물론 별 문제없이 디벨롭 성공하긴 했지만..) 내 로컬 리액트는 18버전인데 16이나 17버전과 피어되지 않는다고 떠있었기도 했다.
    
    
    npm  WARN  ERESOLVE overriding peer dependency
    npm  WARN While resolving: react-side-effect@2.1.1
    npm  WARN Found: react@18.1.0
    npm  WARN  node_modules/react
    npm  WARN  react@"18.1.0" from the root project
    npm  WARN 12 more (@emotion/react, @emotion/styled, ...)
    npm  WARN
    npm  WARN Could not resolve dependency:
    npm  WARN  peer  react@"^16.3.0 || ^17.0.0" from react-side-effect@2.1.1
    npm  WARN  node_modules/react-helmet/node_modules/react-side-effect
    npm  WARN  react-side-effect@"^2.1.0" from react-helmet@6.1.0
    npm  WARN  node_modules/react-helmet
    npm  WARN
    npm  WARN Conflicting peer dependency: react@17.0.2
    npm  WARN  node_modules/react
    npm  WARN  peer  react@"^16.3.0 || ^17.0.0" from react-side-effect@2.1.1
    npm  WARN  node_modules/react-helmet/node_modules/react-side-effect
    npm  WARN  react-side-effect@"^2.1.0" from react-helmet@6.1.0
    npm  WARN  node_modules/react-helmet
    
    
 </br>
   
앞전 homebrew로 node를 최신 버전으로 업데이트해서 사용했기에 내 로컬에는 가장 최신인 버전인 18버전으로 설치되어 있었다. 현재(2022.05.30) node.js 공홈에서 소개하는 안정적인 버전은 node16이기 때문에 디벨롭이 되지 않은 것으로 판단하였고 homebrew를 이용하여 **node 버전을 16으로 다운그레이드** 했다.  
- [(참조: stackexchange - how do i downgrade node or install a specific previous version using homebrew)](https://apple.stackexchange.com/questions/171530/how-do-i-downgrade-node-or-install-a-specific-previous-version-using-homebrew)  
- [(참조: stackoverflow - how to downgrade node version )](https://stackoverflow.com/questions/47008159/how-to-downgrade-node-version)
   
    
```
brew search node  # 현재 링크된 노드 및 링크 가능한 노드 확인
>>  node ✔  node@12  node@16 nodenv
    
brew unlink node  # 현재 노드를 언링크
>> Unlinking /usr/local/Cellar/node/18.2.0... 68 symlinks removed.
    
brew install node@16  # 16버전 설치
>> If you need to have node@16 first in your PATH, run:
>> echo 'export PATH="/usr/local/opt/node@16/bin:$PATH"' >> /Users/XXX/.bash_profile
    
vi .bash_profile  # 경로설정 insert PATH
    
brew link node@16  # 16버전으로 링크
>> Error: Could not symlink bin/npm
>> To force the link and overwrite all conflicting files: brew link --overwrite node@16
>> To list all files that would be deleted: brew link --overwrite --dry-run node@16
    
brew link --overwrite --dry-run node@16  # 오버라이트
    
node -v  # 노드 버전 확인
>> v16.15.0  # 다운그레이드

```
</br>
    
노드 버전 다운그레이드 후  해당 개츠비 템플릿 다시 디벨롭해보기.   
`npm rebuild`로 다시 빌드하고 `gatsby clean`으로 캐시를 삭제한 뒤 gatsby develop 성공!
- [(참조: stackoverflow - Error: Module did not self-register)](https://stackoverflow.com/questions/28486891/uncaught-error-module-did-not-self-register)  
- [(참조: gatsby - Troubleshooting Common Errors)](https://www.gatsbyjs.com/docs/how-to/local-development/troubleshooting-common-errors/)
    
```
gatsby develop
>> Error: Module did not self-register:
    
npm rebuild  # 노드 다운그레이드 했으므로 다시 빌드
>> rebuilt dependencies successfully
    
gatsby develop  # 에러..
>> Error: Unable to deserialize cloned data due to invalid or unsupported version.
>> Please run the command with the --verbose flag again.
    
gatsby develop --verbose  # 에러..
>> Error: Unable to deserialize cloned data due to invalid or unsupported version.
>> Please run the command with the --verbose flag again.
    
gatsby clean   # 캐시 삭제
>> info Deleting
>> info Successfully deleted directories
    
gatsby develop  # 디벨롭 성공
>> You can now view zoomkoding.com in the browser. <http://localhost:8000/>
>> View GraphiQL, an in-browser IDE, to explore your site's data and schema. <http://localhost:8000/___graphql>
    
```
</br>
    
[http://localhost:8000/](http://localhost:8000/)
로컬환경에서 템플릿이 떠있는 것을 확인할 수 있다.



</br>
</br>

(추가보충필요)
#### 0. gatsby 소개 
- gatsby 란?
- gatsby 의 특징


<a name="footnote_1">1</a>: Q. 왜 homebrew로 설치할까?

