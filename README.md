# we-code

## 목차
1. [프로젝트 개요](#1-프로젝트-개요)
2. [주요 기능](#2-주요-기능)
3. [DB 구조](#3-db-구조)
4. [API 문서](#4-api-문서)
5. [상세 화면](#5-상세-화면)

<br>

> [최종 발표 PPT](https://docs.google.com/presentation/d/1UbVTZNiwzYlFrY_9wZZicjKhuJtXjC4yo_6-8K3ooOM/edit#slide=id.g27821047df5_0_0)

<br>

# 1. 프로젝트 개요

<br>

<strong>ㆍ 시행처</strong>: [카카오x구름] Spring & React 풀스택 개발자 과정<br><br>
<strong>ㆍ 기간</strong>: 2024.05 ~ 2024.07<br>


<strong>ㆍ 기술 스택 </strong> <br>
| Back-End     | Database         | Deployment                |
|--------------|------------------|---------------------------|
| ![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white) | ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white) ![H2](https://img.shields.io/badge/H2-0078D4?style=for-the-badge&logo=h2&logoColor=white) | ![Kakao krampoline](https://img.shields.io/badge/Kakao%20krampoline-FFCD00?style=for-the-badge&logo=kakao&logoColor=black) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white) ![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white) |


## 팀 구성

| ![yjiiny](https://avatars.githubusercontent.com/u/153581188) | ![OiPKL](https://avatars.githubusercontent.com/u/130027416) | ![jw-park-github](https://avatars.githubusercontent.com/u/165545220) | ![rpghks07](https://avatars.githubusercontent.com/u/2668683) |
| --- | --- | --- | --- |
| [yjiiny](https://github.com/yjiiny) | [OiPKL](https://github.com/OiPKL) | [jw-park-github](https://github.com/jw-park-github) | [rpghks07](https://github.com/rpghks07) |

<br>



# 2. 주요 기능
* 코드(Post) 및 댓글(Comment) CRUD 기능
* 질문(Question) 및 답변(Answer) CRUD 기능
* 회원가입, 로그인, 로그아웃, 회원 정보 관리

<br>

# 3. DB 구조

<br>

<img width="960" alt="ERD" src="https://github.com/code-six/we-code-0509/assets/165545220/74d42c57-966f-4f94-bf18-8e0b4a8998d0"><br>

<br>


### **SiteUser (회원)**

| 필드명 | 자료형 | 제약 조건 | 설명 |
| --- | --- | --- | --- |
| id | Long | PK, Not Null, Increment | 고유값 |
| email | String | Not Null | 이메일 주소 |
| password | String | Not Null | 비밀번호 |
| username | String | Not Null | 닉네임 |

<br>

### **Post (게시글)**

| 필드명 | 자료형 | 제약 조건 | 설명 |
| --- | --- | --- | --- |
| id | Integer | PK, Not Null, Increment | 고유값 |
| subject | String | Not Null | 게시글 제목 |
| author | SiteUser | Not Null | 게시글 작성자 |
| content | String | Not Null | 게시글 내용 |
| createDate | LocalDateTime | Not Null | 게시글 작성일 |
| modifyDate | LocalDateTime | Not Null | 게시글 수정일 |

<br>

### **Comment (댓글)**

| 필드명 | 자료형 | 제약 조건 | 설명 |
| --- | --- | --- | --- |
| id | Integer | PK, Not Null, Increment | 고유값 |
| author | SiteUser | Not Null | 댓글 작성자 |
| content | String | Not Null | 댓글 내용 |
| createDate | LocalDateTime | Not Null | 댓글 작성일 |
| modifyDate | LocalDateTime | Not Null | 댓글 수정일 |

<br>

### **Question (질문)**

| 필드명 | 자료형 | 제약 조건 | 설명 |
| --- | --- | --- | --- |
| id | Integer | PK, Not Null, Increment | 고유값 |
| subject | String | Not Null | 질문 제목 |
| author | SiteUser | Not Null | 질문 작성자 |
| content | String | Not Null | 질문 내용 |
| createDate | LocalDateTime | Not Null | 질문 작성일 |
| modifyDate | LocalDateTime | Not Null | 질문 수정일 |

<br>

### **Answer (답변)**

| 필드명 | 자료형 | 제약 조건 | 설명 |
| --- | --- | --- | --- |
| id | Integer | PK, Not Null, Increment | 고유값 |
| author | SiteUser | Not Null | 답변 작성자 |
| content | String | Not Null | 답변 내용 |
| createDate | LocalDateTime | Not Null | 답변 작성일 |
| modifyDate | LocalDateTime | Not Null | 답변 수정일 |

<br>
<br>

# 4. API 문서

<br>

## AnswerController

| Method | API          | Path                | Query | Body           | Status | JSON Result                   |
|--------|--------------|---------------------|-------|----------------|--------|-------------------------------|
| POST   | Create Answer| /answer/create/{id} | None  | AnswerForm     | 302    | 질문 상세 페이지로 리다이렉트 |
| GET    | Modify Answer Form | /answer/modify/{id} | None | None       | 200    | 답변 수정 폼                   |
| POST   | Modify Answer | /answer/modify/{id} | None  | AnswerForm     | 302    | 질문 상세 페이지로 리다이렉트 |
| GET    | Delete Answer | /answer/delete/{id} | None  | None           | 302    | 질문 상세 페이지로 리다이렉트 |
| GET    | Vote Answer   | /answer/vote/{id}   | None  | None           | 302    | 질문 상세 페이지로 리다이렉트 |

<br>

## CommentController

| Method | API           | Path                  | Query | Body            | Status | JSON Result                   |
|--------|---------------|-----------------------|-------|-----------------|--------|-------------------------------|
| POST   | Create Comment| /comment/create/{postId} | None  | CommentForm    | 302    | 게시물 상세 페이지로 리다이렉트 |
| GET    | Modify Comment Form | /comment/modify/{commentId} | None | None | 200 | 댓글 수정 폼                   |
| POST   | Modify Comment| /comment/modify/{commentId} | None | CommentForm   | 302    | 게시물 상세 페이지로 리다이렉트 |
| GET    | Delete Comment| /comment/delete/{commentId} | None | None         | 302    | 게시물 상세 페이지로 리다이렉트 |
| GET    | Vote Comment  | /comment/vote/{commentId} | None | None          | 302    | 게시물 상세 페이지로 리다이렉트 |

<br>

## MyPageController

| Method | API             | Path                  | Query | Body                         | Status | JSON Result                                       |
|--------|-----------------|-----------------------|-------|------------------------------|--------|---------------------------------------------------|
| GET    | My Page         | /user/mypage          | None  | None                         | 200    | 마이페이지 (사용자 정보, 게시물, 댓글 목록)        |
| POST   | Update Nickname | /user/mypage/updateNickname | None | nickname                 | 200    | 닉네임 변경됨. 5초 후 로그아웃 후 재로그인 필요     |
| POST   | Update Email    | /user/mypage/updateEmail | None | email                     | 200    | 이메일 변경됨                                     |
| POST   | Update Password | /user/mypage/updatePassword | None | currentPassword, newPassword | 200 | 비밀번호 변경됨                                   |
| POST   | Upload Profile  | /user/mypage/uploadProfile | None | MultipartFile file          | 302    | 프로필 이미지 업로드됨                             |

<br>

## PostController

| Method | API            | Path                  | Query | Body       | Status | JSON Result                    |
|--------|----------------|-----------------------|-------|------------|--------|--------------------------------|
| GET    | List Posts     | /post/list            | page, kw | None   | 200    | 게시물 목록 페이지               |
| GET    | Detail Post    | /post/detail/{id}     | None  | None       | 200    | 게시물 상세 페이지               |
| GET    | Create Post Form | /post/create        | None  | None       | 200    | 게시물 생성 폼                   |
| POST   | Create Post    | /post/create          | None  | PostForm   | 302    | 게시물 목록 페이지로 리다이렉트  |
| GET    | Modify Post Form | /post/modify/{id}   | None  | None       | 200    | 게시물 수정 폼                   |
| POST   | Modify Post    | /post/modify/{id}     | None  | PostForm   | 302    | 게시물 상세 페이지로 리다이렉트  |
| GET    | Delete Post    | /post/delete/{id}     | None  | None       | 302    | 게시물 목록 페이지로 리다이렉트  |
| GET    | Vote Post      | /post/vote/{id}       | None  | None       | 302    | 게시물 상세 페이지로 리다이렉트  |

<br>

## QuestionController

| Method | API              | Path                    | Query | Body          | Status | JSON Result                    |
|--------|------------------|-------------------------|-------|---------------|--------|--------------------------------|
| GET    | List Questions   | /question/list          | page, kw | None      | 200    | 질문 목록 페이지               |
| GET    | Detail Question  | /question/detail/{id}   | None  | None          | 200    | 질문 상세 페이지               |
| GET    | Create Question Form | /question/create    | None  | None          | 200    | 질문 생성 폼                   |
| POST   | Create Question  | /question/create        | None  | QuestionForm  | 302    | 질문 목록 페이지로 리다이렉트  |
| GET    | Modify Question Form | /question/modify/{id} | None  | None       | 200    | 질문 수정 폼                   |
| POST   | Modify Question  | /question/modify/{id}   | None  | QuestionForm  | 302    | 질문 상세 페이지로 리다이렉트  |
| GET    | Delete Question  | /question/delete/{id}   | None  | None          | 302    | 질문 목록 페이지로 리다이렉트  |
| GET    | Vote Question    | /question/vote/{id}     | None  | None          | 302    | 질문 상세 페이지로 리다이렉트  |

<br>

## MainController

| Method | API          | Path  | Query | Body | Status | JSON Result                    |
|--------|--------------|-------|-------|------|--------|--------------------------------|
| GET    | Root Redirect| /     | None  | None | 302    | 게시물 목록 페이지로 리다이렉트 |

<br>
<br>

# 5. 상세 화면

<strong>[/post/list]</strong><br>
![메인화면_코드 목록](https://github.com/code-six/we-code/assets/165545220/3e6fceba-c38f-431a-8c00-67e5326506fd)

<strong>[/post/create]</strong><br>
![코드 등록 화면](https://github.com/code-six/we-code/assets/165545220/877320f0-d19b-44f8-a2bd-c32b91a2be46)

<strong>[/question/create]</strong><br>
![질문 등록 화면](https://github.com/code-six/we-code/assets/165545220/ebae0661-b3f7-453a-9c78-fd60e8683b89)

<strong>[/question/list]</strong><br>
![질문 상세 화면](https://github.com/code-six/we-code/assets/165545220/c69962cc-899a-4212-a78e-4aa0cd39a73d)

<strong>[/user/mypage]</strong><br>
![회원 정보 수정](https://github.com/code-six/we-code/assets/165545220/378c6589-e6c0-4b64-a6e3-551c3a998320)

<strong>[/user/signup]</strong><br>
![회원가입](https://github.com/code-six/we-code/assets/165545220/acbeee8c-9561-494f-a2d7-3e8df477d4d4)
