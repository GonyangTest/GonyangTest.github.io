---
layout: post
title:  "깃허브 페이지 Action Workflow 구성"
date:   2025-03-26 16:56:11 +0900
categories: TIL
---

## GitHub Actions 워크플로우 설정

### 1. 워크플로우 파일 생성
`.github/workflows` 디렉토리를 생성하고 그 안에 `deploy.yml` 파일을 만듭니다.

### 2. 워크플로우 내용 작성
```yaml
name: Deploy Jekyll site to Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.2'
          bundler-cache: true
      - name: Setup Pages
        uses: actions/configure-pages@v4
      - name: Build site
        run: bundle exec jekyll build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./_site

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### 3. 워크플로우 설정
1. GitHub 저장소의 Settings > Pages로 이동
2. Build and deployment 섹션에서:
   - Source: GitHub Actions 선택
   - Branch: main 선택
3. Save 버튼 클릭

### 4. 워크플로우 실행 확인
1. Actions 탭에서 워크플로우 실행 상태 확인
2. 배포가 완료되면 지정된 URL에서 사이트 확인 가능

이렇게 설정하면 main 브랜치에 push할 때마다 자동으로 GitHub Pages가 배포됩니다.