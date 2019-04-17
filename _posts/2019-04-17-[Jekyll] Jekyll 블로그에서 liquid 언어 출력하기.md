---
layout: post
title: "Jekyll 블로그의 코드블록에서 liquid 코드 출력하기"
subtitle: "highlight 메서드 내부에서 liquid 코드 실행 정지하기"
tags: Jekyll
author: Nayeong Kim
comments : True
---

<div id='preview' class='display-none'>
Jekyll로 블로그를 만들면 코드블록은 highlight메서드를 사용하여 나타낸다. 다른 언어를 코드블록 내부에서 출력하는 경우 문제가 생기지 않지만 코드블록 내에 liquid 언어를 출력할때 아래와 같은 문제가 발생한다.
</div>




### 1 . raw 메서드 : liquid 코드 실행 정지하기

Jekyll로 블로그를 만들면 코드블록은 highlight메서드를 사용하여 나타낸다. 다른 언어를 코드블록 내부에서 출력하는 경우 문제가 생기지 않지만 코드블록 내에 liquid 언어를 출력할때 아래와 같은 문제가 발생한다.

![before]({{ site.baseurl }}/assets/img/beforeRaw.png)

{% highlight html %}
<p> liquid 테스트 </p>
{% if post.tags %}
<p> post.tags</p>
{% endif %}
{% endhighlight %}

당연히, 코드블록 내부에 텍스트 형식으로 뿌려질 것이라 생각과는 달리,  Jekyll이 markdown을 변환하는 과정에서 liquid 코드를 실행시켜버려 출력되지 않음을 확인 할 수 있다.

<br>

이때 사용할 수 있는 것이 **raw 메서드**이다.

Jekyll은 raw 메서드 안에 있는 내용은 자체적으로 이스케이프 처리하여 텍스트 형식으로 출력이 가능하게 만들어준다.

![after]({{ site.baseurl }}/assets/img/afterRaw.png)
{% highlight html %}
{% raw %}

<p> liquid 테스트 </p>
{% if post.tags %}
<p> post.tags</p>
{% endif %}
{% endraw %}
{% endhighlight %}



<br>

<br>