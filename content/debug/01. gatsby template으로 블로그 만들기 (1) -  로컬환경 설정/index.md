---
emoji: ๐ 
title: gatsby template์ผ๋ก ๋ธ๋ก๊ทธ ๋ง๋ค๊ธฐ(1) - ๋ก์ปฌํ๊ฒฝ ์ค์ 
date: '2022-05-31 23:00:00'
author: hwan
tags: blog gatsby ๊ฐ์ธ ๋น ๋ธ๋ก๊ทธ
categories: Debug
---

#### ๋ชฉ์ฐจ
 1. ๋ก์ปฌ ํ๊ฒฝ ๋ง๋ค๊ธฐ
 2. ๋์ ์ฝ์ง๊ธฐ

</br>
</br>

## 1. ๋ก์ปฌ ํ๊ฒฝ ๋ง๋ค๊ธฐ  

---

**1.1  node, npm, gatsby ์ค์นํ๊ธฐ**

gatsby๋ react.js ๊ธฐ๋ฐ์ผ๋ก node๋ฅผ ์ค์นํด์ผํ๋ค.  
npm์ ์๋ฐ์คํฌ๋ฆฝํธ์ ํจํค์ง ๊ด๋ฆฌ์๋ก ๋์  yarn์ ์ฌ์ฉํ  ์๋ ์๋ค.  

</br>

- homebrew๋ก node.js์ค์น <sup>[1](#footnote_1)</sup>
    - `brew install node@16` 
    - node 16 ๋ฒ์ ์ผ๋ก ์ค์นํ๊ธฐ
    - node 18 ๋ฒ์ ์์ gatsby build error ๋ฐ์ํ๊ธฐ ๋๋ฌธ 

- homebrew๋ก npm ์ค์นํ๊ธฐ
    - `brew install npm`
    - Q. npm์ด ๋ญํ๋๊ฑฐ์ง? -> [(์ฐธ๊ณ : npm๋ฑ ํจํค์ง ๊ด๋ฆฌ์ ์ค๋ช ํฌ์คํธ)](https://yceffort.kr/2022/05/npm-vs-yarn-vs-pnpm)  

- gatsby ์ค์นํ๊ธฐ
    - `brew install g gatsby-cli`

</br>

``` 
brew install node@16  # node 16 ์ค์น
brew install npm  # npm ์ค์น
npm install -g gatsby-cli  # gatsby ์ค์น

#brew install node #๊ฐ์ฅ ์ต์ ์ node๋ก ์ค์น๋จ
```
</br>
</br>

**1.2  ์ ์ค์น๋์๋์ง ๋ฒ์  ํ์ธํ๊ธฐ**


```
node -v  # node ๋ฒ์ ํ์ธ >> v16.15.0
npm -v  # npm ๋ฒ์ ํ์ธ >> 8.10.0
gatsby -v  # gatsby ๋ฒ์ ํ์ธ >> Gatsby CLI version: 4.14.0

```
</br>
</br>

**1.3  ์ ํํ ํํ๋ฆฟ์ ๋ด๊ฐ ์์ํ  ๋๋ ํ ๋ฆฌ์ ํด๋ก ํ๊ธฐ**

- `gatsby new [dir name] [gatsby address]`  

- ๋์ ๊ฒฝ์ฐ ์ค์ฝ๋ฉ ๋์ ํํ๋ฆฟ์ ์ฌ์ฉํ์๋ค.
    - ์ค์ฝ๋ฉ ๋ gatsby ํํ๋ฆฟ : [๋งํฌ](https://github.com/zoomkoding/zoomkoding-gatsby-blog)

</br>

```
# gatsby new hwnm-study <https://github.com/zoomkoding/zoomkoding-gatsby-blog>

```
</br>
</br>

**1.4  ํด๋น ๋๋ ํ ๋ฆฌ์์ ๊ฐ์ธ ๋น ์คํํ๊ธฐ**


- ํด๋น ๋๋ ํ ๋ฆฌ๋ก ์ด๋ํ๊ธฐ
    - `cd [dir name]`

- ๊ฐ์ธ ๋น ์คํํ๊ธฐ
    - `npm install`
    - `gatsby develop`

- ์ ์คํ๋์๋์ง ๋ก์ปฌ ํ๊ฒฝ์์ ํ์ธํ๊ธฐ
    - localhost:8000

</br>

```
# cd hwnm-study

npm install
gatsby develop

```
</br>
</br>

**1.5  (๋ฒ์ธ) ์ค์ฝ๋ฉ๋์ ํํ๋ฆฟ ๋๋ฒจ๋กญ์ ๋ง์ฃผํ๋ ์๋ฌ**


- `gatsby develop`  ํ JavaScript bundle failed ์๋ฌ ๋ฐ์ ์
    - node ๋ฒ์  ํ์ธํ๊ธฐ
    - 18๋ฒ์ ์ด๋ผ๋ฉด 16์ผ๋ก ๋ค์ด๊ทธ๋ ์ด๋ํด์ฃผ๊ธฐ

- `npm install` ํ ๋ฒ์ ์ ๋ฌธ์ ๋ก dependency ์๋ฌ ๋ฐ์ ์
    - `rm package-lock.json` : package-lock.json ์ญ์ ํ๊ธฐ
    - `rm -rf node_modeules` : node_modules ํด๋ ์ญ์ ํ๊ธฐ
    - `npm install --legacy-peer-deps` : dependency ๋ฌด์ํ๊ณ  ์คํํ๊ธฐ

- `gatsby develop`  ํ Module not found ์๋ฌ ๋ฐ์ ์
    - `npm install @emotion/react`, `npm install @emotion/styled` : ๋ถ์กฑํ ๋ชจ๋ ๋ฐ๋ก ์ค์นํ๊ธฐ

- ์ ๊ณผ์  ํ `gatsby develop`  ์ด ์ฌ์ ํ ์คํ๋์ง ์๋๋ค๋ฉด `gatsby clean`๋ก ์บ์๋ฅผ ์ญ์ ํด์ฃผ์

</br>
</br>
</br>
</br>

## ๐  2. ๋์ ์ฝ์ง๊ธฐ
---

> 
> - ๊ธฐ๋ก์ด์ . ์์ ๋ฒ์ธ์์ ์๋ฌ๋ณ ํด๊ฒฐ๋ฐฉ๋ฒ์ ์ ์ด๋จ์ผ๋ ์์ผ๋ก ๋ ํจ์จ์ ์ธ ๋๋ฒ๊น์ ์ํ์ฌ ์ด๋ฒ ๋์ ๋๋ฒ๊น ๊ณผ์ ์ ์์ฐจ์ ์ผ๋ก ๊ธฐ๋กํด๋๋ค. ๋๊ตฐ๊ฐ์๊ฒ ๋ช ๋ถ์ด๋ฉด ๋๋  ๊ณผ์ ์ด๊ฒ ์ง๋ง ๋์๊ฒ ์๋์๋ค. ๋ ๋ง์ด ๋ง์ฃผ์น๋ฉด์ ํจ์จ์ ์ผ๋ก ์ ์ ์๊ฐ์์ ํด๊ฒฐํ  ์ ์๊ธฐ๋ฅผ.
> - **๋ฐฐ์1. ๊ณต์ ๋ฌธ์๋ฅผ ์ฐธ๊ณ ํ์!**  
>    gatsby ๊ณต์ ํํ์ด์ง์ troubleshooting common error ๋ฌธ์์ ๋ด๊ฐ ๋ง์ฃผํ ๋ช ์๋ฌ๋ค์ด ์์๋ค. (๋ชจ๋ ์ค์น, ์บ์ ์ญ์ )
> - **๋ฐฐ์2. ๋ฒ์ ์ ์ ํ์ธํ์!**
> - **๋ฐฐ์3. ์๋ฌ๋ฉ์ธ์ง๋ฅผ ์ ํ์ธํ์!**  
>    ํค์๋๋ฅผ ์ ์ฐพ์ผ๋ฉด stackoverflow์ ํด๋น ์ด์๋ฅผ ๋ง์ฃผ์น๊ณ  ํด๊ฒฐํ ๊ฒฐ๊ณผ๊ฐ ์๋ค.

</br>
</br>

### 2.1 dependency ์๋ฌ

node์ npm, gatsby๊ฐ ์ ์ค์น๋์๋ค. (๋ผ๊ณ  ์๊ฐํ ์ฌ๊ธฐ๊ฐ ๋ฌธ์ ์๋ค..)  
gatsby๋ฅผ ์คํํ  ๋๋ ํ ๋ฆฌ๋ฅผ ์์ฑํด์ฃผ๊ณ  ํด๋น ํํ๋ฆฟ์ ์คํํ๊ธฐ ์ํด ๊ฐ์ ธ์ค๋ ๊ณผ์ ์์ ์๋ฌ๊ฐ ๋ฐ์ํ๋ค.  

```
gatsby new study <https://github.com/zoomkoding/zoomkoding-gatsby-blog>

```


์๋ฌ๋ฅผ ๋ฌด์ํ๊ณ  ์์ฑ๋ node_modulesํด๋์ package-lockํ์ผ(ํด๋น ํํ๋ฆฟ์์ ์จ์ผํ๋ ํจํค์ง๊ฐ package.json์ ์ ํ ์๋ ๋ฐ ๊ทธ๊ฒ๊ณผ ๊ด๋ จํ์ฌ ์๋ชป๋ ๋ถ๋ถ)์ ์ญ์ ํ๊ณ  npm install, npm start๋ฅผ ๊ฐํํ์ง๋ง ์ญ์๋ ๊ณ์ํด์ ์คํ์ด ๋ถ๊ฐํ์๋ค.

```
npm cache clean --force
rm -rf node_modules
rm package-lock.json

```
๋ด๊ฐ ๋ฐ์ ์ฒซ๋ฒ์งธ ์๋ฌ์ฝ๋๋ ์๋์ ๊ฐ๋ค.   
๋ฒ์ ํธํ๋ฌธ์ ์ธ dependency ์๋ฌ์๋ค.  

```
#์ฒซ ์๋ฌ์ฝ๋

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

### 2.2 ๋ด ๋ก์ปฌ์ ๋ฌธ์ ? ์๋๋ฉด gatsby ํํ๋ฆฟ์ ๋ฌธ์ ?

๋ด๊ฐ ์ฌ์ฉํ๋ ค๋ ํํ๋ ์ ๋ฌธ์ ์ธ์ง gatsby์์ฒด๋ฅผ ๋๋ฆฌ์ง ๋ชปํ๋ ๊ฒ์ธ์ง ํ์ธํ๊ธฐ ์ํด  
gatsby ๊ณต์ ํํ์ด์ง์์ ์ ๊ณตํ๋ ํํ๋ฆฟ์ ๋ก์ปฌ์์ ์๋ํด๋ณด๊ธฐ๋ก ํ๋ค.

> [ ๋ฒ์  ํ์ธ ]  
> node -v    : v18.2.0  
> npm -v    : 8.10.0  
> gatsby -v     : Gatsby CLI version: 4.14.0  
>   
</br>


```
#๋ค๋ฅธ ํํ๋ฆฟ ๋ก์ปฌ์ ํด๋ก 
gatsby new gatsby-casper <https://github.com/scttcper/gatsby-casper>

```
</br>


dependency๊ด๋ จ ๋ฌธ์ ๊ฐ ์์ง๋ง ์๋ฌ๊ฐ ์๋๋ผ ๊ฒฝ๊ณ ์ด๊ณ ,  
gatsby์ฌ์ดํธ๋ฅผ ๋๋ฒจ๋กญํ๋๋ฐ ์ฑ๊ณตํ๋ค.

```
#๊ฒฝ๊ณ 
npm  WARN  ERESOLVE overriding peer dependency
.
.

#๋๋ฒจ๋กญ ์ฑ๊ณต
Your new Gatsby site has been successfully bootstrapped. Start developing it by running:

cd gatsby-casper
gatsby develop

```
</br>

localhost:8000์ผ๋ก ์ ์ํ์ฌ ํ๋ฉด์ด ์ ๋์ค๋ ๊ฒ์ ํ์ธ.  
์ด๋ก์จ ๋ด ๋ก์ปฌํ๊ฒฝ์์ gatsby๋ฅผ ๋๋ฆฌ๋ ๋ฐ ๋ฌธ์ ๊ฐ ์๋ค๋ ๊ฒ์ ํ์ธํ๋ค.  
๋ค์ zoomkoding๋์ ํํ๋ฆฟ์ ์คํํ๊ธฐ ์ํด ๋๋ฒ๊น์ ํด๋ณด์.

</br>
</br>


### 2.3 zoomkoding ํํ๋ฆฟ ๋ค์ ์๋

</br>

**2.3.1 ์ค์ฝ๋ฉ ํํ๋ฆฟ ํด๋ก  ํ npm install**  

: ๋๋ฒจ๋กญ ํ  ์ ์๋ค
    
    
    gatsby new study <https://github.com/zoomkoding/zoomkoding-gatsby-blog>
    
    cd study  # ํด๋น ๋๋ ํ ๋ฆฌ๋ก ์ด๋
    gatsby develop
    >> ERROR
    >> There was a problem loading the local develop command. Gatsby may not be installed in your site's "node_modules" directory.
    >> Perhaps you need to run "npm install"? You might need to delete your "package-lock.json" as well.
    
    rm package-lock.json  # ์๋ฌ์์ ๋งํ๋๋ก ์ญ์ 
    rm -rf node_modeules  # ์ ๋๋ก ์ค์น๋์ง ์์์ผ๋ฏ๋ก ์ญ์ 
    
    npm install
    >> WARN
    >> Some issues need review, and may require choosing
    
    gatsby develop
    >> ERROR
    >> Generating development JavaScript bundle failed
    
    
</br>
</br>
    
**2.3.2. ํจํค์ง ์คํ ์ dependency ๋ฌด์ํ๊ณ  ์งํํ๊ธฐ** 

- ```npm install --legacy-peer-deps```  
    - dependency ๋ฌด์ํ๊ณ  ์งํํ๊ธฐ
    - [(์ฐธ๊ณ : npm install `-force` and `-legacy-peer-deps` ์ฐจ์ด์ )](https://velog.io/@yonyas/Fix-the-upstream-dependency-conflict-installing-NPM-packages-%EC%97%90%EB%9F%AC-%ED%95%B4%EA%B2%B0%EA%B8%B0)  


- `npm install @emotion/react`, `npm install @emotion/styled` 
    - ๋๋ฒจ๋กญ ์ ๋ชจ๋์ด ์์, ๊ทธ ๋ชจ๋ ๋ฐ๋ก ์ค์น


: ํ์ง๋ง ์ฌ์ ํ ๋๋ฒจ๋กญ ํ  ์ ์๋ค.


    
    
    rm package-lock.json && rm -rf node_modeules  # ์ ๋จ๊ณ์์ gatsby developํ๋ฉด์ ๋ ์์ฑ๋์ผ๋ฏ๋ก ๋ค์ ์ญ์ 
    
    npm install --legacy-peer-deps  # dependency ๋ฌด์ํ๊ณ  ์งํ
    >> WARN
    >> Some issues need review, and may require choosing a different dependency.
    
    gatsby develop
    >> ERROR
    >> Module not found: Error: Can't resolve '@emotion/react'
    >> Module not found: Error: Can't resolve '@emotion/styled'
    
    npm install @emotion/react # ๋ชจ๋ ๋ฐ๋ก ์ค์น
    npm install @emotion/styled
    
    gatsby develop
    >> ERROR
    >> Generating development JavaScript bundle failed
    
    
</br>
</br>
    


**2.3.3. node ๋ฒ์  ๋ฐ๊พธ๊ธฐ**

: ๋ธ๋ ๋ฒ์  16์ผ๋ก ๋ฐ๊พผํ ๋๋ฒจ๋กญ ์ฑ๊ณต
    
 ์ด ํํ๋ฆฟ์ ์ฌ์ฉํ ํ๊ธฐ๋ ์ฐพ์ ๋ณด๋ฉด์ ์์๊น์ง์ ๋๋ฒ๊น์ด ๋น์ทํ๋ฐ ์ ๋ด ๋ก์ปฌ์์  ์๋ ๊น ์๊ฐํ๋ค๊ฐ..  
 ์ฌ๊ธฐ์ ๋ถํฐ ๋ธ๋๋ฒ์ ์ ๋ฌธ์ ๋ผ๋ ๊ฒ์ ๊นจ๋ฌ์๋ค.
    
    gatsby develop
    >> ERROR: Generating development JavaScript bundle failed

</br>
    
์ ์๋ฌ๋ก ๊ฒ์ํ๋ ๋ธ๋ 18๋ก ๊ฐ์ธ ๋น๋ฅผ ์ฌ์ฉํ๋ค๊ฐ ํด๋น ์ด์์ ์ง๋ฉดํ ์ผ์ด์ค๊ฐ ์์๋ค.  
- [(์ฐธ์กฐ: stackoverflow -  gatsby build error webpack related maybe)](https://stackoverflow.com/questions/71991480/gatsby-build-error-webpack-related-maybe)
    
๋งจ ์ฒ์ ์๋ฌ ํ, ๋ฌธ์ ๊ฐ ๋ก์ปฌ์ธ์ง ํํ๋ฆฟ์ธ์ง ํ์ธํ  ๋ gatsby-casper ํํ๋ฆฟ ์คํ์ ๋ฐ์๋ ๊ฒฝ๊ณ ์์๋ (๋ฌผ๋ก  ๋ณ ๋ฌธ์ ์์ด ๋๋ฒจ๋กญ ์ฑ๊ณตํ๊ธด ํ์ง๋ง..) ๋ด ๋ก์ปฌ ๋ฆฌ์กํธ๋ 18๋ฒ์ ์ธ๋ฐ 16์ด๋ 17๋ฒ์ ๊ณผ ํผ์ด๋์ง ์๋๋ค๊ณ  ๋ ์์๊ธฐ๋ ํ๋ค.
    
    
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
   
์์  homebrew๋ก node๋ฅผ ์ต์  ๋ฒ์ ์ผ๋ก ์๋ฐ์ดํธํด์ ์ฌ์ฉํ๊ธฐ์ ๋ด ๋ก์ปฌ์๋ ๊ฐ์ฅ ์ต์ ์ธ ๋ฒ์ ์ธ 18๋ฒ์ ์ผ๋ก ์ค์น๋์ด ์์๋ค. ํ์ฌ(2022.05.30) node.js ๊ณตํ์์ ์๊ฐํ๋ ์์ ์ ์ธ ๋ฒ์ ์ node16์ด๊ธฐ ๋๋ฌธ์ ๋๋ฒจ๋กญ์ด ๋์ง ์์ ๊ฒ์ผ๋ก ํ๋จํ์๊ณ  homebrew๋ฅผ ์ด์ฉํ์ฌ **node ๋ฒ์ ์ 16์ผ๋ก ๋ค์ด๊ทธ๋ ์ด๋** ํ๋ค.  
- [(์ฐธ์กฐ: stackexchange - how do i downgrade node or install a specific previous version using homebrew)](https://apple.stackexchange.com/questions/171530/how-do-i-downgrade-node-or-install-a-specific-previous-version-using-homebrew)  
- [(์ฐธ์กฐ: stackoverflow - how to downgrade node version )](https://stackoverflow.com/questions/47008159/how-to-downgrade-node-version)
   
    
```
brew search node  # ํ์ฌ ๋งํฌ๋ ๋ธ๋ ๋ฐ ๋งํฌ ๊ฐ๋ฅํ ๋ธ๋ ํ์ธ
>>  node โ  node@12  node@16 nodenv
    
brew unlink node  # ํ์ฌ ๋ธ๋๋ฅผ ์ธ๋งํฌ
>> Unlinking /usr/local/Cellar/node/18.2.0... 68 symlinks removed.
    
brew install node@16  # 16๋ฒ์  ์ค์น
>> If you need to have node@16 first in your PATH, run:
>> echo 'export PATH="/usr/local/opt/node@16/bin:$PATH"' >> /Users/XXX/.bash_profile
    
vi .bash_profile  # ๊ฒฝ๋ก์ค์  insert PATH
    
brew link node@16  # 16๋ฒ์ ์ผ๋ก ๋งํฌ
>> Error: Could not symlink bin/npm
>> To force the link and overwrite all conflicting files: brew link --overwrite node@16
>> To list all files that would be deleted: brew link --overwrite --dry-run node@16
    
brew link --overwrite --dry-run node@16  # ์ค๋ฒ๋ผ์ดํธ
    
node -v  # ๋ธ๋ ๋ฒ์  ํ์ธ
>> v16.15.0  # ๋ค์ด๊ทธ๋ ์ด๋

```
</br>
    
๋ธ๋ ๋ฒ์  ๋ค์ด๊ทธ๋ ์ด๋ ํ  ํด๋น ๊ฐ์ธ ๋น ํํ๋ฆฟ ๋ค์ ๋๋ฒจ๋กญํด๋ณด๊ธฐ.   
`npm rebuild`๋ก ๋ค์ ๋น๋ํ๊ณ  `gatsby clean`์ผ๋ก ์บ์๋ฅผ ์ญ์ ํ ๋ค gatsby develop ์ฑ๊ณต!
- [(์ฐธ์กฐ: stackoverflow - Error: Module did not self-register)](https://stackoverflow.com/questions/28486891/uncaught-error-module-did-not-self-register)  
- [(์ฐธ์กฐ: gatsby - Troubleshooting Common Errors)](https://www.gatsbyjs.com/docs/how-to/local-development/troubleshooting-common-errors/)
    
```
gatsby develop
>> Error: Module did not self-register:
    
npm rebuild  # ๋ธ๋ ๋ค์ด๊ทธ๋ ์ด๋ ํ์ผ๋ฏ๋ก ๋ค์ ๋น๋
>> rebuilt dependencies successfully
    
gatsby develop  # ์๋ฌ..
>> Error: Unable to deserialize cloned data due to invalid or unsupported version.
>> Please run the command with the --verbose flag again.
    
gatsby develop --verbose  # ์๋ฌ..
>> Error: Unable to deserialize cloned data due to invalid or unsupported version.
>> Please run the command with the --verbose flag again.
    
gatsby clean   # ์บ์ ์ญ์ 
>> info Deleting
>> info Successfully deleted directories
    
gatsby develop  # ๋๋ฒจ๋กญ ์ฑ๊ณต
>> You can now view zoomkoding.com in the browser. <http://localhost:8000/>
>> View GraphiQL, an in-browser IDE, to explore your site's data and schema. <http://localhost:8000/___graphql>
    
```
</br>
    
[http://localhost:8000/](http://localhost:8000/)
๋ก์ปฌํ๊ฒฝ์์ ํํ๋ฆฟ์ด ๋ ์๋ ๊ฒ์ ํ์ธํ  ์ ์๋ค.



</br>
</br>

(์ถ๊ฐ๋ณด์ถฉํ์)
#### 0. gatsby ์๊ฐ 
- gatsby ๋?
- gatsby ์ ํน์ง


<a name="footnote_1">1</a>: Q. ์ homebrew๋ก ์ค์นํ ๊น?

