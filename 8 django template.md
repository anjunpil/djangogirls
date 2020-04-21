## 템플릿 동적 데이터

- `post_list` 를 view에서 보여주고 전달하기 위해선 모델을 가져와야한다

- `views.py` 에 추가사항 입력

  ```python
  from .models import Post #models에 class Post를 가져와 사용함
  from django.utils import timezone #timezone 모듈을 불러온다
  
  def post_list(request):
      posts =Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
      return render (request,'blog/post_list.html',{'posts':posts})
  #posts key값으로 html에 불러오겠다 
  
  ```

  

## 장고 템플릿

	#### 템플릿 태그

- 브라우저는 HTML만 알고 있어 템플릿 태그를 넣어 동적인 웹사이트를 만들어 줄 수 있다

- {{posts}} 처럼 넣어 표시 해줘야 함

  ```html
  {% for post in posts%}
  	<p>publised_date : {{post.published_date}}</p>
      <h1><a href="">{{post.title}}</a></h1>
      <p>{{post.text|linebreaksbr}} #행바뀜을 문단으로 변환하도록 하라
  {% endfor %} #for 문을 돌려 쿼리문안의 object들을 가져온다
  ```
  
 

  

