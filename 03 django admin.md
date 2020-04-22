## 장고 관리자

- `LANGUAGE_CODE='en-us'` 를 `ko` 로 변경

- blog/admin.py 로 들어가 변경

  ```python
  from django.contrib import admin
  form .models import Post
  
  admin.site.register(Post)
  ```

  - 관리자 모드에 Post 모델 등록

- 그 전에 슈퍼유저 생성

  ```shell
  python manage.py creatsuperuser
  ```

  

