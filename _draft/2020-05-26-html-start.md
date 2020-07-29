---

title: "HTML 이란?"
excerpt: "HTML시작"
categories:
  - HTML
tags:
  - HTML
  - Web
  - Front-End
last_modified_at:  2020-05-26T03:57:00

---

# HTML

- **웹페이지를 나타내는 정보**
- 명심해야할것은 똑같은 결과물을 만들수 있더라도 **태그의 의미** 를 활용하여
 **웹페이지 정보를 우선적으로 표현해야한다.**



## Tag
- 통계에 따르면 **약 25개의 태그** 를 사용하는 웹페이지가 많다.
- `<a href="">`
  - **(HyperText Reference) link** 를 통해 모든 웹페이지가 연결될수있다는 점에서 가장 의미있는 태그.
- 이외의 필요한 태그는 검색

![tagFrequency](/assets/img/tagFrequency.JPG)
[https://css-tricks.com/average-web-page-data-analyzing-8-million-websites/](https://css-tricks.com/average-web-page-data-analyzing-8-million-websites/)

---

|tag|function|
|:----:|:----:|
|head|Contains metadata/information for the document|
|html|Defines the root of an HTML document|
|body|Defines the document's body|
|title|Defines a title for the document|
|meta|Defines metadata about an HTML document|
|div|Defines a section in a document|
|a|Defines a hyperlink|
|script|Defines a client-side script|
|link|Defines the relationship between a document and an external resourse(most used to link to style sheets)|
|img|Defines an image|
|p|Defines a paragraph|
|span|Defines a section in a document|
|li|Defines a list item|
|ul|Defines an unordered list(the parent tag of li tag)|
|ol|Defines an ordered list(the parent tag of li tag)|
|br|Defines a single line break|
|style|Defines style information for a document|
|h1~h6|Defines HTML headings 1~6|
|input|Defines an input control|
|form|Defines an HTML form for user input|
|strong| Defines important|
|table|Defines a table|
|tbody|Groups the body content in a table|
|tr|Defines a row in a table|
|td|Defines a cell in a table|

[http://w3schools.com/tags](http://w3schools.com/tags)


## Structure

~~~ html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>

  </body>
</html>
~~~

## Attribute
- Tag만으론 정보가 부족한 경우, **Attribute** 를 이용하여 **추가적인 정보** 를 준다.

---
~~~ html
<img src="" width=""></img>
~~~
