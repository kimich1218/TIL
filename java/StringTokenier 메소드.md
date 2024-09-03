### StringTokenizer 클래스란?
- `StringTokenizer` 클래스는 문자열을 우리가 지정한 구분자로 쪼개주는 클래스이다. 그렇게 쪼개 문자열을 토큰이라고 부른다.
- `Bufferedreader` 클래스를 통해서는 라인 단위로 읽을 수 밖에 없어서 쪼갤 수 없는 것을 `StringTokenzier`이 대신 해준다.

### StringTokenizer 생성하는 방식이 무엇이 있을까?
1. 띄어쓰기 기준으로 문자열 분리
```java
String str = "This is coding test study";

System.out.println("==========띄어쓰기 기준============");
StringTokenizer st = new StringTokenizer(str);

while (st.hasMoreTokens()) {
    System.out.println(st.nextToken());
}


```
```
==========띄어쓰기 기준============
This
is
coding
test
study
```

2. 구분자를 기준으로 문자열 분리
```java
String str = "This-is-coding-test-study";

System.out.println("==========구분자 기준============");
StringTokenizer st = new StringTokenizer("-");

while (st.hasMoreTokens()) {
    System.out.println(st.nextToken());
}


```
```
==========구분자 기준============
This
is
coding
test
study`
```

3. 구분자 기준 + true
```java
String str = "This-=is-=coding-test-study";

System.out.println("==========구분자 기준============");
StringTokenizer st = new StringTokenizer(str, "-=", true);

while (st.hasMoreTokens()) {
    System.out.println(st.nextToken());
}

```
```
==========구분자 기준============
This
-
=
is
-
=
coding
-
test
-
study
```
true로 설정할 경우 delim값에 지정된 값은 토큰에 지정된다.

4. 구분자 기준 + false
```java
String str = "This-=is-=coding=test-study";

System.out.println("==========구분자 기준============");
StringTokenizer st = new StringTokenizer(str, "-=", false);

while (st.hasMoreTokens()) {
    System.out.println(st.nextToken());
}

```
```
==========구분자 기준============
This
is
coding
test
study
```
false로 설정할 경우 delim값에 지정된 값은 토큰에 들어가지 않는다.

### 자주 쓰이는 StringTokenizer 메서드
1. hasMoreTokens(): 남아있는 토큰 있으면 true, 없으면 false를 리턴한다.
2. nextToken(): 객체에서 다음 토큰을 리턴한다.
3. countTokens(): 총 토큰의 개수를 리턴한다.
