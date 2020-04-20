## 장고 뷰 만들기 & HTML 시작하기

####  간단한 view 만들어보기

- `blog/views.py`에 간단하게 만들어보기

  ```python
  def post_list(request):
      return render(request,'blog/post_list.html',{})
  #요청(request)을 넘겨 받아 render method를 호출 후에 post_list 템플릿을 보여줌
  ```

  

## HTML

- chrome 이나 firefox,sapari 같은 웹 브라우저가 해석할 수 있는 간단한 코드
- html(hypertext markup language)
  - markup - 누군가 해석하도록 표시(mark)했다는 뜻
  - tag - <(여는태그)></(닫는태그)>, markup의 element이다

- `blog/templates/blog` 폴더 생성해 html을 저장
  - 이렇게 설정하는 이유? 폴더 구조가 복잡해 질 때 좀 더 쉽게 찾기 위해 사용

```html
<html>
    <p>hi</p>
    <p>hello</p>
</html>
```

#### head & body

- head : 문서 정보를 가지고 있지만 보이지 않는 정보들을 담는 영역
- body : 웹 페이지에 직접적으로 보이는 내용이 들어감

```html
<html>
    <head>
        <title>junpil's blog</title>
    </head>
    <body>
        <p>hi</p>
        <p>hello</p>
    </body>
</html>
```

- `<h1>,<h2>,<h3>`  :큰 제목, 중 제목, 소 제목	

- `<em>`: 텍스트 기울기

- `<strong>` : 텍스트를 두껍게

- `<br>` : 줄바꿈, 스스로 닫히는 태그 속성 사용 x

- `<a href: http>` : 하이퍼 링크 걸기

- `<ul> `: 목록 만들기

- `<div>`: 페이지 섹션

  - [div자세한 내용](https://coding-factory.tistory.com/188)

    

#### post_list.html 만들어보기

```html
<html>
    <head>
        <title>Django Girls Blog</title>
    </head>
    <body>
        <div>
            <h1>
                <a href="">Django Girls Blog</a>
            </h1>
        </div>
        <div>
            <p>published: 14.06.2014, 12:14</p>
            <h2><a href="">My first post</a></h2>
            <p>Aenean eu leo quam. Pellentesque ornare sem lacinia quam venenatis vestibulum. Donec id elit non mi porta gravida at eget metus. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus.</p>
        </div>
        <div> <p>published: 14.06.2014, 12:14</p>
            <h2><a href="">My second post</a></h2>
            <p>Aenean eu leo quam. Pellentesque ornare sem lacinia quam venenatis vestibulum. Donec id elit non mi porta gravida at eget metus. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut f.</p>
        </div>
    </body>
</html>
```



- 3개의 div 섹션이 있음, 두 div는 블로그 게시일과 블로그 제목 링크가 있음

