## CSS 만들기

- 부트스트랩을 사용함

- `post_list.html` 에 부트스트랩 링크를 넣어 글꼴,색 등 정적인 부분을 불어옴

  ```python
  <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
  <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
  ```

![css](C:\Users\sky\Pictures\djangogirls\css.PNG)

- 정적폴더 static을 blog 폴더안에 만들고 링크 없이 css를 불러올 수 있게 만듦

- `#`으로 시작해 알파벳,숫자 중 6개를 조합해 헥사코드로 나타냄

  ```css
  h1 a {
      color: #FCA205;
  }
  ```

- h1 a 는 CSS 셀렉터, h1 요소 안 a요소를 넣어 스타일을적용할 수 있음
- a,h1,body 뿐만 아니라 class,id 속성에 의해서 요소를 식별
- `post_list`에 정적파일을 로딩
- `<head></head> ` 사이에 blog/css파일을 불러옴

```html
{% load static %}
<link rel ="stylesheet" href = "{% static 'css/blog.css '%}">
```

```css
body {
    padding-left: 25px;
} #왼쪽 여백을 25px 남기겠다
```

```html
	<link href="//fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext" rel="stylesheet" type="text/css"> #lobster 라는 글꼴을 링크로 가져옴
```

```html
<div class="page-header">
    <h1><a href="/">Django Girls Blog</a></h1>
</div>  #class를 상단으로 명해줌
<div class="post">
    <p>published: {{ post.published_date }}</p>
    <h1><a href="">{{ post.title }}</a></h1>
    <p>{{ post.text|linebreaksbr }}</p>
</div> #기재할 수 있도록 post로 명해줌
```

