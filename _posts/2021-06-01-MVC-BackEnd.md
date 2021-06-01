---
layout: post
title: Spring MVC 구조
subtitle: BackEnd study
categories: BackEnd
tags: [BackEnd, MVC]
---

## Spring MVC (Model View Controller)
Spring MVC는 mvc 패턴기반의 웹 프레임워크다.


### Model
어플리케이션 정보, 데이터 처리관리, 
* 사용자가 사용하는 모든 데이터 정보를 가지고있는 컴포넌이며, View나 Controller의 어떤 정보도 알수없어야한다.
* 변경이 일어나면 처리방법을 구현해야한다

### View
사용자 인터페이스, 사용자에게 보여짐
* Model이 가지고있는 데이터를 저장하면 안된다
* Model이나 Controller의 정보를 알면 안되며 단순히 표시해주는 역할을 가지고있다
* 변경이 일어나면 처리방법을 구현해야한다

### Controller
Model과 View간의 상호동작 조정과 연결
*Model 또는 View에 대한 정보를 알아야한다
*model 또는 View의 변경을 인지하여 대처를 해야한다


### Component 정리
|-------------------|----------------------------------------------------|
|DispatcherServlet| 모든 요청을 최초로 받아들이는 역할|
|Controller| 요청을 실제로 처리하는 역할|
|HandlerMapping| 클라이언트 요청을 처리할 Controller를 찾는 작업처리|
|View| 응답하는 로직을 처리|
|ViewPeslover| 응답할 View를 찾는 작업을 처리|
|ModelAndView| 컨트롤러의 처리결과로써 응답에 사용할 데이터와 뷰에대한 정보 집합|



