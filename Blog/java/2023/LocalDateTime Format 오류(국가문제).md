# 2023-07-19 LocalDateTime Format 오류(국가문제)

```java
String dateString = "05:53:55.041 AM 07/13/2023";
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("hh:mm:ss.SSS a MM/dd/yyyy")
LocalDateTime localDateTime = LocalDateTime.parse(dateString, formatter);
System.out.println(localDateTime);
```

java에서 "05:53:55.041 AM 07/13/2023" 형식의 String 데이터를 LocalDateTime으로 변환하려 할 때 다음의 오류가 발생하였다.

`Text '05:53:55.041 AM 07/13/2023' could not be parsed at index 13`

해당 인덱스에 해당하는 'A'에서 오류가 발생하였는데, 해당 오류에 대해 찾아봐도 무엇이 문제인지 알 수 없었다.

그래서 역으로 LocalDateTime을 해당 formatter 형식으로 출력해보니 한글 포멧의 형태로 "05:53:55.041 오전 07/13/2023"로 출력하고 있었고,
거기서 힌트를 얻어 다음과 같이 .withLocale(Locale.US) 를 사용하여 영문 형태로 변환하였더니 잘 동작하였다.

```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("hh:mm:ss.SSS a MM/dd/yyyy").withLocale(Locale.US);
```