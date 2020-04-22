## 장고 폼

- Post 모델에 적용할 ModelForm을 생성해 자동으로 모델에 결과물을 저장할 수 있음

- `form.py` 파일을 만듦

```python
from django import forms
from .models import Post #model을 불러옴

#새 class를 만듦
class PostForm(forms.ModelForm):
    class Meta:
        model =Post
        fields = ('title','text',)  #title과 text만 보여지게 함
```

-`base.html` 에 링크를 추가해 + 버튼을 생성

```python
<a href="{% url 'post_new' %}" class="top-menu"><span class="glyphicon glyphicon-plus"></span></a>
```

- urls.py 에 새로운 path를 지정해줌

```python
path('post/new',views.post_new,name='post_new'),
```

- views 에 추가
- `form` 으로 필요한 필드만 선정해서 post_edit로 렌더링 해준다

```python
def post_new(request):
    form = PostForm()
    return render(request, 'blog/post_edit.html', {'form': form})
```

- post_edit.html
- `{% csrf_token %}` 보안유지를 위해
- {{ form.as_p }} 폼이 보이게 간단히 만듦
- `save` 저장 버튼 추가

```html
{% extends 'blog/base.html' %}

{% block content %}
    <h1>New post</h1>
    <form method="POST" class="post-form">{% csrf_token %}
        {{ form.as_p }}
        <button type="submit" class="save btn btn-default">Save</button> 
    </form>
{% endblock %}
```

#### 폼 저장하기

- 폼을 제출할 때 같은 뷰를 불러옴, `request` 에는 우리가 입력했던 데이터들을 가지고 있음 `request.POST`가 이 데이터를 가지고 있다
- `<form>` 정의로 넘겨진 폼 필드의 값들은 `request.POST`에 저장 

```python
if request.method == "POST":
    [...]
else:
    form =PostForm()
```

- 첫번째 - 처음 페이지에 접속했을 때, 새글을 쓸 수 있게 폼을 비워둠
- 두번째 - 폼에 입력된 데이터를 view 페이지로 가지고 올때 조건문(if)을 사용해서 가지고 옴

```python
form = PostForm(request.POST)
```



- 등록된 request.POST를 폼으로 변수 form에 저장

- `form.is_valid`를 이용해 잘못된 값이 있는지 확인
- `form.save()` 로 폼을 저장하는 작업과 작성자를 추가하는 작업
- `PostForm` 에는 작성자(author) 필드가 없다,
- `commit=False` 작성자 정보를 추가, 저장 

```python
if form_is_valid():
    post = form.save(commit=False)
    post.author= request.user
    post.published_date = timezone.now()
    post.save()
```

```python
from django.shortcuts import redirect
 
return redirect('post_detail',pk=post.pk)
#돌아갈 경로를 지정해줌
```

## 폼 수정하기

```python
<a class="btn btn-default" href="{% url 'post_edit' pk=post.pk %}"><span class="glyphicon glyphicon-pencil"></span></a>
```

- 연필 버튼을 만들어 post_edit.html로 이동, pk값을 post.pk로

```python
 path('post/<int:pk>/edit/', views.post_edit, name='post_edit'),
```

- views.post_edit로 경로지정

```python
def post_edit(request, pk):
    post = get_object_or_404(Post, pk=pk)
    if request.method == "POST":
        form = PostForm(instance=post)
        if form.is_valid():
            post = form.save(commit=False)
            post.author = request.user
            post.published_date = timezone.now()
            post.save()
            return redirect('post_detail', pk=post.pk)
    else:
        form = PostForm(instance=post)
    return render(request, 'blog/post_edit.html', {'form': form})
```

- Post모델에 ,pk는 현재 pk로 post변수값으로 지정
- `POST` 요청을 받으면 현재 pk값에 PostForm이라는 class에 넣어 특정 필드만 뽑아 form 변수에 지정
- post는 form.save로 저장
- `redirect` detail.html로 돌아가고 pk값은 현재 pk값으로 저장
- 후에 post_edit로 요청받아 렌더링해줌

## 보안

- 로그인한 유저만 보이도록 변경

```python
{% if user.is_authenticated %}
    <a href="{% url 'post_new' %}" class="top-menu"><span class="glyphicon glyphicon-plus"></span></a>
{% endif %}
```

