---
layout: post
title: "Git commit author(작성자) 변경하기"
subtitle: "git rebase 명령을 이용한 커밋 수정하기"
tags: Bixbys
author: Nayeong Kim
comments : True
---

<div id='preview' class='display-none'>
커밋 후 푸시를 완료했어도 contribution에 반영되지 않고 있어 원격지의 commit을 살펴보았다. author(작성자)가 달라서 생기는 문제였음을 확인할 수 있다. 사실 예전에도 이런 에러를 마주한 적이 있었는데, git을 처음 사용하던 때라 commit과 push 외에 다른 명령어를 사용한다는 것이 두려워 해결하지 못했었다. 오늘, 같은 문제를 마주한 김에 이를 해결해보았다.
</div>

커밋 후 푸시를 완료했어도 contribution에 반영되지 않고 있어 원격지의 commit을 살펴보았다. 

![커밋 에러]({{ site.baseurl }}/assets/img/commitErr1.png)

author(작성자)가 달라서 생기는 문제였음을 확인할 수 있다.

> 사실 예전에도 이런 에러를 마주한 적이 있었는데, git을 처음 사용하던 때라 commit과 push 외에 다른 명령어를 사용한다는 것이 두려워 해결하지 못했었다. 
> 
> 아래는 예전의 잘못된 커밋 로그이다.
>
> ![커밋에러]({{ site.baseurl }}/assets/img/commitErr2.png)

오늘, 같은 문제를 마주한 김에 이를 해결해보았다.

<br/>
<br/>

## commit author(작성자) 수정
이런 현상은 왜 일어나는 것일까? 로컬에서 사용자의 정보(user.name, user.email)가 잘못 설정되어(혹은 설정을 안했거나) 있기 때문이다.

`git config --list`명령을 통해 설정값을 확인할 수 있다.

<br/>

### 1. git config
사용자 정보가 잘못 저장되어 있다면 이를 변경 혹은 생성하자.
{% highlight shell %}
# 사용자 이름 변경
$ git config --global user.name "{사용자 이름}"

# 사용자 이메일 변경
$ git config --global user.email "{사용자 이메일}"
{% endhighlight %}
위 과정은 commit을 수정하는 과정과는 무관하지만, 이후의 commit을 작성할때 같은 실수가 반복되지 않기 위해 해주는 과정이다.

<br/>

### 2. git rebase 란?
말 그대로 re-base 한다고 생각하면 된다. 즉, branch의 base를 다시 설정한다는 의미이다.
<br/>
또한, `rebase`는 `merge`와 달리, 별도의 merge commit을 생성하지 않는다.

위와 같은 특징으로 인해 `rebase`는 기존의 commit log를 단장하거나 재정렬할때 쓰인다. 즉, `rebase`는 기존의 commit을 수정할 수 있는 명령일 것이다. 때문에 `rebase`를 사용하면 기존 commit의 내용 뿐만아니라 author(작성자)까지도 변경이 가능하다.

<br/>

### 3. git rebase로 commit author 수정
author가 잘못된 commit을 보내게 되면 contribution에 반영되지 않는다.

![커밋에러]({{ site.baseurl }}/assets/img/commitErr3.png)

![contribution]({{ site.baseurl }}/assets/img/contribution.png)

1월 16일에 보낸 commit이 contribution에 적용되지 않았음을 확인할 수 있다.

<br/>

#### 3-1. 기준 commit 찾기
git log를 통해 **수정하고 싶은 commit의 바로 전 commit의 hash값을 복사**해온다.
{% highlight shell %}
$ git log 
{% endhighlight %}

![복사할 commit]({{ site.baseurl }}/assets/img/commitLog.png)

<br/>

#### 3-2. git rebase
{% highlight shell %}
$ git rebase -i {commit hash}
{% endhighlight %}

{% highlight shell %}
# 아래와 같은 내용이 나오면 수정하고 싶은 commit에 edit을 붙여준다.
edit 01234 samsung sw expert academy  #pick => edit
edit 01235 2019.01.06 algorithm       #pick => edit
pick 01236 2019.01.17 Algorithm

# Rebase 01233..82e7c9c onto 01233 (61 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
{% endhighlight %}

이렇게 하고 나면 edit을 표시한 commit에 대한 rebase가 진행된다.

<br/>

#### 3-3. author 수정
{% highlight shell %}
$ git commit --amend --author="{사용자 이름 <사용자 이메일>}"
{% endhighlight %}

이렇게 입력하고 나면 커밋에 대한 에디터 창이 뜨게되는데 마찬가지로 :wq로 수정사항을 저장한다.

rebase를 진행할 commit이 더 있다면 아래 명령어를 입력하고 `3-3`과정을 반복한다.
{% highlight shell %}
$ git rebase --continue
# 더이상 진행할 rebase가 없는 경우 아래 내용이 출력된다.
Successfully rebased and updated refs/heads/master.
{% endhighlight %}

<br/>

#### 3-4. 원격 저장소(github)에 push
git push 명령을 사용하면  rejected가 발생하면서 push되지 않는다. f 옵션을 추가하여 강제로 push 한다.
{% highlight shell %}
$ git push -f
{% endhighlight %}

<br/>

성공적으로 commit author가 변경되었음을 확인할 수 있다. 또한 contribution에도 수정된 commit 2개가 추가되었다.

![변경된log]({{ site.baseurl }}/assets/img/commitSuc.png)

![변경된contribution]({{ site.baseurl }}/assets/img/contribution2.png)