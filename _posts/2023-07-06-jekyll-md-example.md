---
title: "Jekyll Markdown 기반 포스트 작성 예제"

categories: [Jekyll]

tags: [Jekyll, Markdown, Post]

last_modified_at: 2023-07-06T00:00:00-00:00
---

# 1. 메타데이터
## 1.1. 포스트 설정
```
---
title: "제목"

categories: [카테고리]

tags: [태그1, 태그2, 태그3]

last_modified_at: 2023-07-06T00:00:00-00:00
---
```
> 이 외에도 다양한 메타데이터가 있지만, 가능하면 _config.yml로 옮겨서 전역적으로 설정하는 편이 좋을 것 같다.

# 2. 본문
## 2.1. Header
 * 문서 제목
 ```
 This is an H1
 =============
 ```

This is an H1
=============
 
 * 문서 부제목
 ```
 This is an H2
 -------------
 ```
 
This is an H2
-------------
 > Jekyll은 메타데이터에 title 속성을 제공하기에 위의 두 개는 잘 사용하지 않을 것 같다.

 * 글머리
 ```
 # This is a H1
 ## This is a H2
 ### This is a H3
 #### This is a H4
 ##### This is a H5
 ###### This is a H6
 ```
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6

## 2.2. BlockQuote
```
> This is a first blockqute.
>   > This is a second blockqute.
>   >   > This is a third blockqute.
```
> This is a first blockqute.
>   > This is a second blockqute.
>   >   > This is a third blockqute.

# 참고할 만한 자료
 * [Markdown Guide](https://www.markdownguide.org/getting-started/)

# 참고자료
 * [마크다운(Markdown) 사용법](https://gist.github.com/ihoneymon/652be052a0727ad59601)
 * [하우투: 같이 따라하기 시리즈](https://devinlife.com/howto/)