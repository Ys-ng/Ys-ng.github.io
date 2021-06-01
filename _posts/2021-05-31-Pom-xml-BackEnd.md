---
layout: post
title: pom.xml
subtitle: BackEnd study
categories: BackEnd
tage: [BackEnd]
---

### POM ( Project Object Model )
POM은 프로젝트의 구조와 내용을 설명하고 있으며 pom.xml 파일에 프로젝트 관리 및 빌드에 필요한 환경 설정, 의존성 관리 등의 정보들을 기술합니다.

### XML( eXtensible Markup Language )
XML은 데이터 저장과 전송을 목적으로 만들어진 마크업 언어이다. HTML과 달리 정해진 태그를 쓰지않고 사용자가 태그를 정의해서 사용할수있다.
특정 어플리케이션에 종속되어있지 않고, 데이터를 가지고있을뿐 어떤 작동을 하는것은 아니다.




### 태그정리
```xml
<modelVersion>4.0.0</modelVersion>
```
POM모델 버전

```xml
<groupId>com.yangs</groupId>
```
화사나 제작사 프로젝트 이름

```xml
<artifactId>Test</artifactId>
```
프로젝트에 할당된 고유이름

```xml
<name>Test</name>
```
보통 아티팩트ID와 동일함

```xml
<version>1.0.0-BUILD-SNAPSHOT</version>
```
프로그램 버전

```xml
<packaging>jar</packaging>
```
패키지 종류, jar, zip. web일경우 war.


```xml
<properties>
		<java-version>1.6</java-version>
		<org.springframework-version>5.2.15.RELEASE</org.springframework-version>
		<org.aspectj-version>1.6.10</org.aspectj-version>
		<org.slf4j-version>1.6.6</org.slf4j-version>
</properties>
```
이 pom.xml에서 사용하는 속성값 등을 모아둠. 필요에따라 바뀜

```xml
<dependencies> ...... 의존 라이브러리 정보 ...... </ dependencies>
```
의존 라리브러리. 이 프로그램이 참조하는 Java 기본 시스템을 제외한 라이브러리. 자동으로 기록되기때문에 편집하지않음.

```xml
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-jdbc</artifactId>
	<version>${org.springframework-version}</version>
</dependency>
```
라이브러리 정보. 그룹ID, 아티팩트ID, 버전, 범위를 포함.  `dependencies` 태그안에 있어야한다.
이 정보들은 https://mvnrepository.com/ 에서 검색한다(위 예시 https://mvnrepository.com/artifact/org.springframework/spring-context/5.2.15.RELEASE)




