---
title: "Jekyll Markdown 기반 포스트 작성 예제"

categories: [ETC, Jekyll]

tags: [Markdown, Post]

last_modified_at: 2023-07-06T00:00:00-00:00
---

# 1. 메타데이터
## 1.1. 포스트 설정

-------

```
---
title: "제목"

categories: [TOP_CATEGORIE, SUB_CATEGORIE]

tags: [TAG1, TAG2, TAG3]

last_modified_at: 2023-07-06T00:00:00-00:00
---
```

-------

> 이 외에도 다양한 메타데이터가 있지만, 가능하면 _config.yml로 옮겨서 전역적으로 설정하는 편이 좋을 것 같다.

-------

# 2. 본문
## 2.1. Header

-------

### 2.1.1. 문서 제목

 ```
 This is a H1
 =============
 ```
 
This is a H1
=============

-------

### 2.1.2. 문서 부제목

 ```
 This is a H2
 -------------
 ```
 
This is a H2
-------------

-------

 > Jekyll은 메타데이터에 title 속성을 제공하기에 위의 두 개는 잘 사용하지 않을 것 같다.

-------

### 2.1.3. 글머리

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

-------

 > header는 특별한 의미가 있어서 그런지 앞에 공백을 포함한 문자가 오면 인식되지 않는다.

-------

## 2.2. BlockQuote

-------

### 2.2.1. 블럭 인용

 ```
 > This is a first blockqute.
 >   > This is a second blockqute.
 >   >   > This is a third blockqute.
 ```
 > This is a first blockqute.
 >   > This is a second blockqute.
 >   >   > This is a third blockqute.

-------

### 2.2.2. 혼합 블럭 인용

 ```
 > ### This is a H3
 > * List
 >   ```
 >   code
 >   ```
 ```
 > ### This is a H3
 > * List
 >   ```
 >   code
 >   ```

-------

## 2.3. List

-------

### 2.3.1. 순서있는 목록

 ```
 1. 첫 번째
 2. 두 번째
 3. 세 번째
 ```
 1. 첫 번째
 2. 두 번째
 3. 세 번째

-------

### 2.3.2. 순서없는 목록

 ```
 * 빨강
     * 녹색
         * 파랑
 + 빨강
     + 녹색
         + 파랑
 - 빨강
     - 녹색
         - 파랑
 * 빨강
     - 녹색
         * 파랑
             - 주황
 ```

* 빨강
    * 녹색
        * 파랑
+ 빨강
    + 녹색
        + 파랑
- 빨강
    - 녹색
        - 파랑
* 빨강
    - 녹색
        * 파랑
            + 주황

-------

## 2.4. 코드

-------

### 2.4.1. 들여쓰기

```
This is a normal paragraph:

    This is a code block.

end code block.
```

This is a normal paragraph:

    This is a code block.

end code block.

-------

### 2.4.2. 코드블럭

 * `<pre><code>{code}</code></pre>` 방식

 ```
 <pre>
 <code>
 public class BootSpringBootApplication {
    public static void main(String[] args) {
        System.out.println("Hello, Honeymon");
    }
 }
 </code>
 </pre>
 ```
 
 <pre>
 <code>
 public class BootSpringBootApplication {
    public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
    }
 }
 </code>
 </pre>
 
 * 코드블럭코드("```") 방식

 ```
    ```java
    public class BootSpringBootApplication {
        public static void main(String[] args) {
            System.out.println("Hello, Honeymon");
        }
    }
    ```
 ```

```java
public class BootSpringBootApplication {
    public static void main(String[] args) {
        System.out.println("Hello, Honeymon");
    }
}
```

-------

## 2.5. 수평선

```
* * *

***

*****

- - -

-----
```

* * *

***

*****

- - -

-----

-------

## 2.6. 링크

 * 참조 링크

 ```
 Link: [Google][googlelink]

 [googlelink]: https://google.com "Go google"
 ```

 Link: [Google][googlelink]

 [googlelink]: https://google.com "Go google"

 * 외부 링크

 ```
 [Google](https://google.com, "Go google")
 ```

 [Google](https://google.com, "Go google")

 * 자동 연결

 ```
 * 외부 링크: <http://example.com>
 * 이메일 링크: <address@example.com>
 ```

 * 외부 링크: <http://example.com>
 * 이메일 링크: <address@example.com>

-------

## 2.7. 강조

```
*single asterisks*
_single underscores_
**double asterisks**
__double underscores__
~~cancelline~~
```

*single asterisks*  
_single underscores_  
**double asterisks**  
__double underscores__  
~~cancelline~~  

-------

## 2.8. 이미지

```
![](/path/to/img.jpg)
![](/path/to/img.jpg){: .align-center}
![Alt text](/path/to/img.jpg "Optional title")

#사이즈 조절이 필요한 경우 html 이용
<img src="/path/to/img.jpg" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="RubberDuck"></img><br/>
<img src="/path/to/img.jpg" width="40%" height="30%" title="px(픽셀) 크기 설정" alt="RubberDuck"></img>
```

-------

## 2.9. 표 만들기
```
 * 전체 중앙 정렬

| 항목 | 가격 | 개수 |
|:---:|:---:|:---:|
| 라면 | 800원 | 10개 |
| 과자 | 900원 | 20개 |

 * 개수 중앙 정렬

| 항목 | 가격 | 개수 |
|:---:|:---:|---:|
| 라면 | 800원 | 10개 |
| 과자 | 900원 | 20개 |
```

 * 전체 중앙 정렬

| 항목 | 가격 | 개수 |
|:---:|:---:|:---:|
| 라면 | 800원 | 10개 |
| 과자 | 900원 | 20개 |

 * 개수 우측 정렬
 
| 항목 | 가격 | 개수 |
|:---:|:---:|---:|
| 라면 | 800원 | 10개 |
| 과자 | 900원 | 20개 |

-------

## 2.10. 줄 바꿈

줄 바꿈을 하려면 문장 마지막에 2칸이상을 띄어쓰기 하면 된다.

-------

> 작성하면서 문법이 뭔가 애매하다 싶으면 엔터나 개행을 하는 편이 좋은 것 같다는 생각이 들었다.

-------

# * 참고할 만한 자료

 * [Markdown Guide](https://www.markdownguide.org/getting-started/)
 * [Chirpy Blog](https://chirpy.cotes.page/)

-------

# * 참고자료

 * [마크다운(Markdown) 사용법](https://gist.github.com/ihoneymon/652be052a0727ad59601)
 * [하우투: 같이 따라하기 시리즈](https://devinlife.com/howto/)