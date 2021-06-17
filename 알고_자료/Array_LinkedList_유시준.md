# Array와 List

## 개요
> 
Array와 List에 대해 알아보자

## Array
Array란 배열을 의미한다.
배열은 index가 있고 index에 대응하는 데이터가 있는 자료구조이다.
선형자료구조이며 랜덤액세스가 가능한 자료구조이다.
흔히 자바에서는 primitive type의 변수들의 배열을 선언할 때의 자료구조이다. 
또한 reference type의 변수들의 배열은 ArrayList에 해당한다.

배열의 구조는 아래와 같다. k번 index에 일련의 데이터가 들어가있는 구조이다.
아래의 그림에서는 0번인덱스에서 "a"의 데이터가 1번인덱스에는 "b"의 데이터가 들어가있다.
* 시간 복잡도
> 
삽입 : O(n)
삭제 : O(n)
접근 : O(1)
검색 : O(n)

![](https://images.velog.io/images/dbtlwns/post/4e6cc5c8-4e46-4f5b-a474-54ce05a19f80/image.png)

# List

아래는 링크드 리스트의 구조를 그림으로 나타내었다.
링크드 리스트는 Array처럼 연속된 자료구조가 아니고 데이터와 next 데이터를 가리키는 포인터로 구성된 자료구조이다. 
랜덤 액세스가 불가능하기 때문에 접근을 하려면 O(n)이라는 시간복잡도가 걸린다.
삽입과 삭제는 그 기능자체로는 O(1)이라는 시간 복잡도를 갖지만 해당 위치를 찾아야 하기 때문에 그 동작과 합쳐진다면 O(n)이 걸린다.
* 시간 복잡도
> 
삽입 : O(n)
삭제 : O(n)
접근 : O(n)
검색 : O(n)


![](https://images.velog.io/images/dbtlwns/post/f96e74b6-5f9b-4237-ba61-640c8892ae47/image.png)
더블 링크드 리스트는 링크드 리스트와 다른점 이라면 previous데이터를 가리키는 포인터도 가지고 있다는 점이다. 그대신 그만큼의 메모리 공간이 필요하다.
![](https://images.velog.io/images/dbtlwns/post/e5e761a9-de14-4dc3-9b79-a66369a8f5bb/image.png)
시간 복잡도 측면에서 정리해보면 다음과 같다.
시간 복잡도로만 본다면 O(n)으로 링크드 리스트가 좋지 않아 보이지만 
어디까지나 최악의 경우이고 삽입/삭제가 빈번하다면 링크드리스트를 사용하는게 좋다.
또한 메모리여유가 있다면 더블링크드리스트가 더 좋다고 볼 수 있다. 
반대로 삽입/삭제가 적고 탐색이 많다면 배열이 적당한 자료구조라고 볼 수 있다.


![](https://images.velog.io/images/dbtlwns/post/fd3da532-7f3b-49c4-937a-02fdd376310e/image.png)
