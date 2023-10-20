
`create-react-app`으로 생성된 React 프로젝트를 GitHub Pages에 배포하는 과정을 단계별로 설명드리겠습니다.

1. **프로젝트 초기화:** 만약 아직 `create-react-app`으로 프로젝트를 생성하지 않았다면, 다음 명령어로 생성하세요:
    
    bashCopy code
    
    `npx create-react-app my-app cd my-app`
    
2. **GitHub 저장소 초기화:** 프로젝트 폴더 내에서 Git을 초기화하고 원격 GitHub 저장소를 연결하세요:
    
    bashCopy code
    
    `git init git remote add origin [your-github-repo-url.git]`
    
3. **`gh-pages` 패키지 설치:** `gh-pages`는 GitHub Pages 배포를 도와주는 패키지입니다. 이를 설치하세요:
    
    bashCopy code
    
    `npm install gh-pages --save-dev`
    
4. **`package.json` 수정:** `package.json` 파일을 열고, `"homepage"` 필드를 추가하세요. 이는 프로젝트의 GitHub Pages URL을 지정합니다:
    
    jsonCopy code
    
    `"homepage": "https://[your-github-username].github.io/[repo-name]/"`
    
    그런 다음 `scripts` 섹션에 배포용 스크립트를 두 개 추가하세요:
    
    jsonCopy code
    
    `"scripts": {   // ... 기존 스크립트들   "predeploy": "npm run build",   "deploy": "gh-pages -d build" }`
    
5. **배포:** 다음 명령어를 사용하여 프로젝트를 GitHub Pages에 배포하세요:
    
    bashCopy code
    
    `npm run deploy`
    
6. **GitHub 설정 확인:** GitHub 웹사이트에서 프로젝트의 저장소로 이동하고, `Settings` 탭으로 이동한 다음, `GitHub Pages` 섹션을 찾아 배포 설정이 올바른지 확인하세요. `Source`가 올바른 브랜치(`gh-pages` 브랜치)를 가리키고 있는지 확인하세요.
    
7. **배포된 사이트 확인:** 지정한 `homepage` URL(`https://[your-github-username].github.io/[repo-name]/`)로 접속하여 배포된 사이트를 확인하세요.
    

이제 프로젝트가 GitHub Pages에 성공적으로 배포되었습니다! 원격 저장소에 푸시할 때마다 `npm run deploy`를 실행하여 변경 사항을 GitHub Pages에 쉽게 업데이트할 수 있습니다.

배포사이트 업데이트 하는 명령어 : npm run deploy