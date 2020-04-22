# 장고 모델

- `객체지향프로그래밍` 이란? 모든 것을 하나하나 지시하는 것 대신,모델을 만들어 모델이 어떤 역할을 가지고 어떻게 행동해야 하는지 정의하여 상호작용 할 수 있도록 만드는것
- `객체` 란? 속성과 행동을 모아놓은 것

- 속성 : 객체속성(properties), 행위 :method

#### 어플리케이션 만들기

```shell
python manage.py startapp blog
```

```pytho
INSTALLED_APPS =[
	'blog',
]
```

- setting.py 에서 app 추가해주기

#### 블로그 글 모델 작성

```python
from django.conf import settings #해당위치의 global settings 내용
from django.db import models
from django.utils import timezone #시간 method

#항상 class 이름은 대문자로 시작!!
class Post(models.Model):
    author = models.ForeignKey(setting.AUTH_USER_MODEL, 			 	 on_delete=models.CASCADE)
    #Foreingky - 다른 모델의 대한 링크
    title = models.CharField(max_length=200)
    creadted_date =models.DateTimeField(default=timezone.now)
    #default값은 현재로 설정
    published_date =models.DateTimeField(blank=True,null=True)
    #publish날짜 설정,빈칸 허용,빈값 허용
    
    def publish(self):
        self.published_date =timezone.now()
        self.save()
    def __str__(self):
        return self.title
    
```

*추가*

- django 모델 구현 시 ForeignKeyField를 사용할 일이 많음
- 참조무결성 
  - 기본 키와 참조 키 간의 관계가 항상 유지됨
  - 참조되는 테이블의 행을 참조키가 존재하는 한 삭제 x, 기본키 변경도 x

- models.CASCADE : FK가 바라보는 값이 삭제될 때 모델.instance도 삭제됨
  - PROTECT : FK가 바라보는 값이 삭제될 때 삭제되지 않도록 ProtectError 발생시킴
  - SET_NULL :삭제될 때 FK값을 null로 바꾼다 (null=True)일 때만 가능
  - SET_DEFAULT : 삭제될 때 FK값을 default 값으로 바꿈
  - SET() : 삭제될 때 FK값을 SET에 설정된 함수 등에 의해 설정됨
  - DO_NOTHING : FK 값이 삭제될 때 아무런 행동도 x,참조무결성을 해칠 위험있음

#### 데이터베이스에 모델을 위한 테이블 만들기

-  `python manage.py makemigrations` 로 변경점 확인
- `python manage.py migrate blog` 로 변경점 저장

