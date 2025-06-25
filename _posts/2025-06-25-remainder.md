---
title: "jekyll 기억할 것들"
# categories: [jekyll]
# tags: [jekyll, post]
typora-root-url: ../
author: "KSE"
description: jekyll로 블로그 작성하기 위해 기억할 내용들
toc: true
---



## Server Local에서 Host하기

1. PowerShell에서 asdf178.github.io 폴더로 경로 이동하기
2. bundle exec jekyll s 또는 bundle exec jekyll serve 입력하기
3. http://127.0.0.1:4000/ 열기

## Post 작성하기

1. _posts 폴더 아래에 년도-월-일-제목.md 형식의 파일 만들기

2. Front Matter에 title, categories, tags와 같은 기본 정보 설정하기

   ```yaml
   ---
   title: 제목
   categories: [Top_Category, Sub_Category] # up to 2 elements
   tags: [tag1, tag2, ...] # TAG names should always be lowercase. 0~INFINITY
   author: 작성자 이름(KSE)
   description: Short summary of the post. # or the first words of the post are used.
   typora-root-url: ../
   date: YYYY-MM-DD HH:MM:SS
   toc: false # If you want to turn off TOC(Table of Contents) for a specific post, add this line.
   pin: true # Pin one or more posts to the top of the home page
   ---
   ```

3. 내용 작성하기

## author 추가하기

1. _data/authors.yml에 새로운 author 정보 추가하기

2. Front Matter의 author에 작성자 이름(KSE) 적기

   ```yaml
   ---
   author: <author_id> # for single entry
   # or
   authors: [<author1_id>, <author2_id>]   # for multiple entries
   ---
   ```

