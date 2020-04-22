## 장고 ORM과 쿼리셋

#### 쿼리셋이란?

- 쿼리셋은 전달받은 모델의 객체목록 : 필터를 걸거나 정렬을 할 수 있음

```shell
python manage.py shell
>>>Post.objects.all() #model Post의 모든 객체 조회
<QuerySet [<Post: my post title>, <Post: another post title>]>
>>>Post.objects.create(author=me,title='sample text') #새객체 생성
from django.contrib.auth.models import User #me가 없으므로 User를 불러와야 함
>>> User.objects.all()
<QuerySet [<User: hhjg627>]>
>>> me = User.objects.get(username='hhjg627') #변수 값을 username에서 불러와 지정
>>> Post.objects.all()
<QuerySet [<Post: my post title>, <Post: another post title>, <Post: Sample title>]> #새로 추가가 된 것을 확인 할 수 있음
```

#### 필터링 하기

```shell
>>> Post.objects.filter(author=me)
[<Post: Sample title>, <Post: Post number 2>, <Post: My 3rd post!>, <Post: 4th title of post>]
#username이 me 인 것들만 필터링 해준다
>>> Post.objects.filter(title__contains='title')
[<Post: Sample title>, <Post: 4th title of post>]
#title에 'title'글자가 포함된 글들을 뽑는다
# 장고 ORM은 이름과 연산자의 필터를 밑줄 2개를 사용해 구분!!

>>> from django.utils import timezone
>>> Post.objects.filter(published_date__lte=timezone.now())
[]
# 추가한 게시물을 확인 , 하지만 없어서 빈 list 출력

>>> post =Post.objects.get(title='sample title') #saple title을 얻어옴
>>> post.publish #게시함
>>> Post.objects.filter(published_date__lte=timezone.now())
[<Post: Sample title>] #새로 추가된 게시물을 확인 할 수 있다
```

#### 정렬하기

```shell
>>> Post.objects.order_by('created_date')
[<Post: Sample title>, <Post: Post number 2>, <Post: My 3rd post!>, <Post: 4th title of post>] 
#created_field로 정렬을 해줄 수 있다
# - 를 추가해 반대로 정렬 가능 '-created_date'
```

#### 쿼리셋 연결하기

```shell
>>> Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
# 쿼리셋들을 chaining 할 수 있다
>>> exit()
```

- orm(object relational mapping), 객체-관계 매핑
  - 객체와 관계형 데이터베이스 데이터를 자동으로 mapping(연결)해준다
  - 객체지향DB은 *class* 사용 관계형DB *테이블* 사용
  - 객체모델과 관계형모델 간 불일치가 존재
  - ORM을 통해 SQL을 자동으로 생성하여 불일치를 해결
  - 객체를 통해 간접적으로 DB data를 다룬다

- ORM 장단점
  - 객체 지향적인 코드로 더 직관적이고 비즈니스 로직에 더 집중
  - ORM을 이용하면 직관적인 코드로 데이터를 조작할 수 있어 개발자가 프로그래밍하는 데 집중 할 수 있도록 도와줌
  - 선언문,할당, 종료 같은 부수적인 코드가 급격히 줄어듬
  - 각종 객체 코드 별도 작성으로 가독성을 올려줌
  - *재사용 & 유지보수* 편리성 증가
  - 매핑정보가 명확,ERD 보는 것에 의존도를 낮출 수 있음
  - DBMS에 대한 종속성이 줄어듬
    - 객체 간 관계를 바탕으로 SQL을 자동으로 생성,RDBMS의 데이터 구조와 객체지향 모델 사이의 간격을 좁힐 수 있다
    - ORM 솔루션은 DB에 종속적 x
    - 솔루션에서 자료형 타입까지 유효하다
    - object에 집중함으로 극단적으로 DBMS를 교체하는 거대한 작업에도 비교적으로 적은 리스크와 시간이 소요
    - 간결하고 빠른 가공이 가능

- 단점
  - 완벽한 ORM으로만 서비스 구현 x
    - 편하지만 설계는 매우 신중하게
    - 프로젝트 복잡성이 커질 수록 난이도 또한 올라감
    - 잘못 구현될 경우 속도 저하 등이 생길  수 있음
    - 대형 쿼리는 별도의 튜닝이 필요한 경우가 있음
    - DBMS의 고유 기능을 이용하기 어렵다
    - 프로시저? 가 많은 시슽메에서 생산성 저하나 리스크가 발생할 가능성O

