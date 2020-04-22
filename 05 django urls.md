## 장고 urls

- URLconf(URLconfiguration) 사용 , URL과 일치하는 view를 찾기 위한 패턴들의 집합

#### 장고 URL 작동 

- `mysite/urls.py` 에서 경로 설정

  ```python
  from django.contrib import admin
  from django.urls import path, include 
  #include - 생성한 app 속 url을 포함한다
  
  urlpatterns = [
      path('admin/',admin.site.urls),
      patin('',include('blog.urls')),
      #화면 메인 페이지를 blog폴더 urls로 띄우겠다
  ]
  ```

#### blog.urls

```python
urlpatterns = [
    path('',views.post_list,name = 'post_list'),
    #views.py에 post_list함수로 불러오겠다 , 이름은 불러오기 편한 이름
]
```

