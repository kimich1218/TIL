# 해시 테이블
### 정의

![alt text](https://github-production-user-asset-6210df.s3.amazonaws.com/82080962/363869144-d7988709-7a21-454a-ad91-440a4ee90d90.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20240903%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240903T064937Z&X-Amz-Expires=300&X-Amz-Signature=cf8ba0c8ac779b57221d058ce18ff0daf723df4d3f6490cfc16ec71641b2a4b3&X-Amz-SignedHeaders=host&actor_id=82080962&key_id=0&repo_id=851395303)

해시 테이블은 **키(Key)** 와 **값(Value)** 쌍으로 데이터를 저장하는 효율적인 자료구조이다. 주로 빠른 데이터 검색, 삽입, 삭제를 위해 사용된다. 해시 테이블은 **키(Key)**, **해시 함수(Hash Function)**, **해시(Hash)**, **값(Value)**, **버킷(Bucket)** 이라는 다섯 가지 주요 구성 요소로 이루어진다.

- **키(Key)**: 데이터를 식별하기 위한 고유한 값으로, 해시 함수에 입력되는 값이다.
- **해시 함수(Hash Function)**: 키를 입력받아 일정한 길이의 해시 값으로 변환해주는 함수이다. 다양한 길이를 가진 키를 일정한 길이를 가지는 해시로 변환하여 저장소를 효율적으로 사용할 수 있게 한다.
* **해시(Hash)**: 해시 함수의 출력 결과물로, 해당 키가 저장될 위치를 결정하는 인덱스 역할을 한다.
* **값(Value)**: 해시 테이블에 저장된 데이터 자체로, 키에 매칭되어 저장된다.
* **버킷(Bucket)**: 해시 테이블에서 값을 저장하는 저장소로, 하나의 버킷에 여러 개의 값이 저장될 수 있다.

### 해시 충돌 (Hash Collision)
![alt text](https://github-production-user-asset-6210df.s3.amazonaws.com/82080962/363870732-53d91f11-0d1d-4023-8542-9ea73b7e0e70.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20240903%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240903T065057Z&X-Amz-Expires=300&X-Amz-Signature=8745eb5f9df3801f2f94efbaff3b327694aba9ca439406258874d8b4f3d38693&X-Amz-SignedHeaders=host&actor_id=82080962&key_id=0&repo_id=851395303)

해시 함수는 동일한 해시 값을 여러 키에 대해 생성할 수 있는데, 이를 **해시 충돌**이라고 한다. 해시 충돌이 발생하면 두 개 이상의 키가 동일한 인덱스를 참조하게 되며, 이를 처리하기 위해 여러 가지 방법이 사용된다.

**해시 충돌 해결 방법**

**1. 분리 연결법(Separate Chaining)**
![alt text](https://github-production-user-asset-6210df.s3.amazonaws.com/82080962/363870880-55b0b6ae-1b1e-4c3d-8f6f-202474e1f71f.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20240903%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240903T065145Z&X-Amz-Expires=300&X-Amz-Signature=ada5b249214919d74888ac7f29d79bc443a4b3ca28ded4c9afd62f83979ee33a&X-Amz-SignedHeaders=host&actor_id=82080962&key_id=0&repo_id=851395303)

분리 연결법은 동일한 해시 값을 가진 키들을 연결 리스트로 연결하여 하나의 버킷에 저장하는 방법이다. 충돌이 발생하면 해당 버킷에 새로운 데이터를 리스트의 형태로 추가한다. 이 방법은 해시 테이블의 크기와 상관없이 비교적 간단하게 충돌을 처리할 수 있다.

**2. 개방 주소법(Open Addressing)**
개방 주소법은 충돌이 발생하면 해시 테이블 내의 다른 빈 버킷을 찾아 데이터를 저장하는 방법이다. 이를 구현하는 주요 방법은 다음과 같다:

- **선형 조사(Linear Probing)**: 충돌이 발생한 버킷 이후의 버킷들을 순차적으로 탐색하여 빈 자리를 찾는다.
- **이차 조사(Quadratic Probing)**: 충돌이 발생한 위치에서 제곱 수만큼 떨어진 위치를 탐색하여 빈 자리를 찾는다.
- **이중 해싱(Double Hashing)**: 두 번째 해시 함수를 사용하여 새로운 해시 값을 계산하고, 해당 위치에 데이터를 저장한다.

### 시간 복잡도
해시 테이블에서 키를 통해 값을 찾는 작업은 일반적으로 **O(1)**의 시간 복잡도를 가진다. 이는 해시 함수가 키를 직접 인덱스로 변환하여 값을 즉시 찾아낼 수 있기 때문이다. 하지만, 해시 충돌이 발생하여 충돌 해결 과정이 필요할 때는 최악의 경우 **O(N)**의 시간 복잡도가 발생할 수 있다.