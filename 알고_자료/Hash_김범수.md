### Hash Table
  
  - Hash Table 개념
    - Key와 Value를 1:1로 연관지어 저장하는 자료구조 (연관 배열 구조)
    - Key를 이용하여 Value 도출
    
  - Hash Table 기능
    - 연관배열 구조와 동일한 기능 지원
    - key, Value가 주어졌을 때, 두 값을 저장
    - Key가 주어졌을 때, 해당 Key에 연관된 Value 조회
    - 기존 Key에 새로운 Value가 주어졌을 때, 기존 Value를 새로운 Value로 대체
    - Key가 주어졌을 때, 해당 Key에 연관된 Value 제거

  - HashTable 구조

  - Key
    - 고유한 값
    - 저장 공간의 효율성을 위해 Hash Function에 입력하여 Hash로 변경 후 구성
      - Key는 길이가 다양해서 그대로 저장하면 다양한 길이만큼 저장소 
     
  - Hash Function
    - Key를 Hash로 바꿔주는 역할
    - 해시 충돌(서로 다른 Key가 같은 Hash가 되는 경우)이 발생할 확률을 최대한 줄이는 함수를 만드는 것이 중요
    
  - Hash
    - Hash Function의 결과
    - 저장소에서 Value와 매칭되어 저장
    
  - Value
    - 최종적으로 저장되는 값
   
  - Hash 충돌
    - 서로 다른 Key가 Hash Function에서 중복 Hash로 나오는 경우
    - 충돌이 많아질수록 탐색의 시간 복잡도가 O(1)에서 O(n)으로 증가
    
  - HashTable 장점
    - 적은 리소스로 많은 데이터를 효율적으로 관리 가능
    - 배열의 인덱스를 사용하기 때문에 빠른 검색, 삽입, 삭제 (O(1))
      - HashTable의 경우 인덱스는 데이터의 고유 위치이기 대문에 삽입, 삭제시 다른 데이터를 이동할 필요가 없음
    - Key와 Hash에 연관성이 없어 보안 유리
    - 데이터 캐싱에 많이 사용
    - 중복 제거 유용
  
  - HashTable 단점
    - 충돌 발생 가능성
    - 공간 복잡도 증가
    - 순서 무시
    - 해시 함수에 의존
