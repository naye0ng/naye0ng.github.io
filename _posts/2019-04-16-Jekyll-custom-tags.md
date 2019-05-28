---
layout: post
title: "Jekyll 블로그 커스터마이징 1 - 태그(Tag)"
subtitle: "Jekyll 블로그 목록에 태그 추가하기"
categories : Jekyll
tags: Jekyll
author: Nayeong Kim
comments : True
---


type-theme가 제공하는 Post 목록은 제목, 날짜, 내용 요약 정도만 보여준다. 개인적으로 Post목록에 tag 리스트도 보여주는 것이 좋을 듯 하여 코드를 수정해 보았다.

먼저, **수정 전**의 모습이다.

![before]({{ site.baseurl }}/assets/img/beforeTag.png)

<br>

### 1). Tag 목록 출력하기

태그를 수정하기에 앞서 tag목록이 표시될 페이지를 찾는다. type-theme의 경우, _layouts폴더의 home.html 부분에 있다.
<br>
(Jekyll의 liquid 문법이 Django와 유사하여 빠르게 찾을 수 있었다.)

{% highlight html %}
{% raw %}

<div class="home">
  ...
  <div class="posts">
    {% for post in paginator.posts %}
    <div class="post-teaser">
      <header>   
        <h3 class='mb-0'>
          <a class="post-link" href="{{ post.url | relative_url }}">
            {{ post.title }}
          </a>
        </h3>
        <span class="meta">
          {{ post.date | date: "%B %-d, %Y" }}
        </span>

        <!-- 여기에 tag 추가 -->
        {% if post.tags %}
        {% for tag in post.tags %}
        <span class='tag_box'>{{ tag }}</span>
        {% endfor %}
        {% endif %}
        <!-- tag 추가 끝 -->
    
      </header>
      ...
    </div>
    {% endfor %}
  </div>
</div>
{% endraw %}
{% endhighlight %}
for post in paginator.posts 문의  paginator는 _config.yml에서 설정한 한 번에 보여질 포스팅 목록 이다. 
<br>
즉, paginator.posts는 정해진 수만큼 보여질 Post 정보를 담고 있는 list라고 볼 수 있으며, for문을 통해 post 변수에 paginator.posts의 정보(post 1개)를 넘긴다.

각 post 변수 안에는 이전에 게시한 게시글 정보(제목, 링크, 날짜, 태그 등)가 모두 들어가 있다. 실제로 위 코드에서 post변수를 통해 post.title, post.link를 통해 제목과 링크를 출력하고 있다.
<br>
따라서, 우리가 출력할 복수개의 태그 정보 또한 post 변수가 가지고 있을 것이며, 조금의 구글링을 통해 .tags로 태그 정보를 받아 올 수 있다는 것을 알았다.

**위의 코드는 if문을 통해 해당 post에 tag정보가 있다면, 해당 태그들을 for문을 통해 출력하도록 만든 코드이다.**

<br>

### 2). 커스텀 스타일 적용하기

태그를 출력하는 span 태그에 tag_box 클래스를 선언해줬다. 개인적으로 생각해둔 tag 스타일이 있어 적용해 보았다.

{% highlight css %}
.tag_box {
  padding : 1px 6px;
  border-radius: 3px;
  background-color: #83aad7;
  color : #ffffff;
  font-size: 11px;
  font-weight: 500;
}
{% endhighlight %}

<br>

결과적으로 아래와 같이 원하는 모습의 태그정보가 출력된다.

![after]({{ site.baseurl }}/assets/img/afterTag.png)

<br>

<br>



