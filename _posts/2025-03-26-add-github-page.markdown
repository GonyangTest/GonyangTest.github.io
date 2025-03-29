---
layout: post
title:  "깃허브 페이지 작성"
date:   2025-03-26 16:56:11 +0900
categories: TIL
---

## 작성 방법

***사전 준비***
1. ruby, rubygems 설치
2. git 설치
3. github 계정

### 1. jekyll 및 Bundle 설치
```
gem install jekyll bundle
```

### 2. jekyll 사이트 생성
```
jekyll new GonyangTest.github.io
cd GonyangTest.github.io
```

### 3. git 초기화
```
git init
git add .
git commit -m "Initial commit"
```

### 4. gitHub 원격 저장소 연결
```
git remote add origin https://github.com/username/GonyangTest.github.io.git
git branch -M main
git push -u origin main
```

### 5. _config 설정
_config.yml 파일에서 다음 설정을 수정합니다:
```yaml
title: GonyangTest
description: My GitHub Pages
baseurl: ""
url: "https://username.github.io"
```

### 6. 배포 및 Github page 설정
1. GitHub 저장소의 Settings 탭으로 이동
2. Pages 섹션에서 Source를 main 브랜치로 설정
3. Save 버튼 클릭
4. 배포가 완료될 때까지 대기 (몇 분 소요될 수 있음)

### 7. 로컬에서 테스트
```
bundle exec jekyll serve
```
이 명령어로 로컬에서 사이트를 미리 확인할 수 있습니다.

### 8. 포스트 작성
_posts 디렉토리에 YYYY-MM-DD-title.md 형식으로 파일을 생성하여 작성합니다.
```markdown
---
layout: post
title: "포스트 제목"
date: YYYY-MM-DD HH:MM:SS +0900
categories: 카테고리
---