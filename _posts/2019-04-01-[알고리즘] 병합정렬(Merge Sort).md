---
layout: post
title: "[알고리즘] 병합정렬(Merge Sort)"
subtitle: "Python을 사용하여 병합정렬 구현하기"
author: Nayeong Kim
tags: [Algorithm, Python]
feature-img: "assets/img/sample_feature_img.png"
---
<div id='preview' class='display-none'>
병합정렬이란, 여러 개의 정렬된 자료의 집합을 병합하여 한 개의 정렬된 집합으로 만드는 방식이다. 자료를 최소 단위의 문제까지 나눈 후에 차례대로 정렬(병합)하여 최종 결과를 얻어 낸다.
</div>

## 1. 병합정렬(Merge Sort)
여러 개의 정렬된 자료의 집합을 병합하여 한 개의 정렬된 집합으로 만드는 방식이다. 자료를 최소 단위의 문제까지 나눈 후에 차례대로 정렬(병합)하여 최종 결과를 얻어 낸다.(top-down방식)


<br/>
### 1-1. 병합정렬 과정

**[예]{69, 10, 30, 2, 16, 8, 31, 22}를 병합정렬하는 과정**
<br/>
(1) 분할 : 전체 자료 집합에 대하여, 최소 크기의 부분집합이 될때까지 분할 작업을 계속한다.
![MergeSort-Divid]({{ site.baseurl }}/assets/img/mergesort01.PNG)

(2) 병합 : 2개의 부분집합을 정렬하면서 하나의 집합으로 병합
![MergeSort-Merge]({{ site.baseurl }}/assets/img/mergesort02.PNG)


<br/>
### 1-2. 병합정렬의 시간복잡도

크기가 n인 배열을 반씩(n/2) 나눈후, 나눈 배열에 대한 재귀함수를 호출한다. 분할된 두개의 배열을 merge할때, 두 배열을 한번씩 비교하게 되므로 총 n번의 비교가 수행된다. *(코드를 보면서 생각하면 이해하기 쉬움)*

n 개의 데이터를 병합정렬하는 시간을 T(n)이라 하면, 병합정렬의 시간복잡도는 T(n) = T(1/2)+T(1/2)+n 이 된다. T(n) = 2T(n/2)+n를 정리하면, 합병정렬의 시간복잡도는 **O(nlogn)**이 된다.


<br/>
## 2. 병합정렬 구현

{% highlight python %}
def mergeSort(arr):
​    if len(arr) <= 1:
​        return arr
​    mid = len(arr) // 2
​    left = mergeSort(arr[:mid])
​    right = mergeSort(arr[mid:])
​    return merge(left, right)

def merge(left, right):
​    result = []
​    # 한쪽이 0이 되면 비교는 끝내고, 남은 부분을 붙여주기만 하면 된다.
​    while len(left) > 0 and len(right) > 0:
​        if left[0] <= right[0]:
​            result.append(left.pop(0))
​        else:
​            result.append(right.pop(0))
​    if len(left) > 0:
​        result.extend(left)
​    elif len(right) > 0:
​        result.extend(right)
​    return result

arr = [69, 10, 30, 2, 16, 8, 31, 22]
print(mergeSort(arr))
{% endhighlight %}

<br/>

### 2-1. 병합정렬 최적화

#### (1).  merge호출 최소화

merge를 호출하기 전에 left[-1]과 right[0]을 비교하여 left[-1] < right[0] 라면, merge를 수행하지 않고 left+right를 반환해 주는 것으로 merge과정을 줄일 수 있다.

{% highlight python %}
def mergeSort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = mergeSort(arr[:mid])
    right = mergeSort(arr[mid:])
    if left[-1] < right[0]: return left + right
    return merge(left, right)
{% endhighlight %}
<br/>
#### (2). 배열 대신 인덱스 활용

merge함수는 호출 될때마다 result배열을 동적으로 생성하여 반환한다. 메모리 효율과 시간이 오래 걸리는 단점이 있다. 그러므로 arr위에서 index로 접근하여 변환하는 함수를 생각해볼 수 있다. merge과정에서 새로운 배열을  생성하지 않으므로 빠르고 효율적이다.