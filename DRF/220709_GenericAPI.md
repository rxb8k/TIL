# Generic API

+ 정의 : 일반적인 CRUD 작업을 처리하는 데에 도움이 되도록 DRF에서 제공하는 클래스 기반 View
+ 반복적인 동작을 줄이고, 간결한 코드를 작성할 수 있도록 도와주는 DRF의 핵심 기능

## Pure Django vs Generic API를 사용한 코드 비교
+ Generics API를 사용하지 않았을 때의 코드 : 모든 필드를 직접 작업해주어야함

    ```
    blog.title = ~
    blog.writer = ~
    ...
    ```

+ Generics API를 사용했을 때의 코드

    ```
    from rest_framework import generics

    class BlogList(generics.ListCreateAPIView):
        queryset=Blog.objects.all()
    ```

# 대표적인 Generic API View의 종류
+ ```APIView```: 기본적인 API 뷰를 생성하는 추상 클래스 -> 상속 받아 확장
+ `GenericAPIView`: DRF의 제네릭 API 뷰를 위한 기본 클래스. 주로 다른 제네릭 뷰 클래스에서 상속받아 사용
+ `ListAPIView`: 리스트 형식의 데이터 조회
+ `CreateAPIView`: C 새로운 개체 생성
+ `RetrieveAPIView`: R 단일 개체에 대한 세부 정보 조회
+ `UpdateAPIView`: U 기존 개체 업데이트
+ `DestroyAPIView`: D 개체 삭제

## Generic API View들의 내장 메서드
+ 다음의 Generic APIView들은, 다음의 내장 메서드에 대한 Method handler를 제공한다.
+ get()을 내장한 API View들은, `get_queryset()`만 있어도 프론트엔드에서 해당 api에 GET 요청을 보내 응답을 받아올 수 있다.
    + get() 메서드를 내장하지 않는 Generic API View: `CreateAPIView`, `UpdateAPIView`, `DestroyAPIView`

|API View|내장 메서드|
|---|---|
|CreateAPIView|post()|
|ListAPIView|get()|
|RetrieveAPIView|get()|
|UpdateAPIView|put(), patch()|
|DestroyAPIView|delete()|
|ListCreateAPIView|get(), post()|
|RetrieveUpdateAPIView|get(), put(), patch()|
|RetrieveDestroyAPIView|get(), delete()|
|RetrieveUpdateDestroyAPIView|get(), put(), patch(), delete()|



## Functions
### get_queryset()
+ 데이터베이스에서 조회할 쿼리셋을 반환
+ `QuerySet`이란 Django에서 데이터베이스로부터 가져온 객체들의 집합으로, 데이터 조회 및 조작에 활용되는 ORM의 핵심 요소

---
### Reference
https://velog.io/@mynghn/%EC%A0%9C%EB%84%A4%EB%A6%AD-%EB%B7%B0%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-API-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0

https://velog.io/@ohwani/Django-DRF-view-of-DRF

https://www.django-rest-framework.org/api-guide/generic-views/#concrete-view-classes