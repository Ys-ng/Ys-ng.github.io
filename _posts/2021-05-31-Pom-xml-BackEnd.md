---
layout: post
title: pom.xml
subtitle: this is a subtitle
categories: BackEnd
tage: Spring
---

POM ( Project Object Model )
POM은 프로젝트의 구조와 내용을 설명하고 있으며 pom.xml 파일에 프로젝트 관리 및 빌드에 필요한 환경 설정, 의존성 관리 등의 정보들을 기술합니다.

태그정리

<modelVersion>4.0.0</modelVersion>
POM모델 버전

<groupId>com.yangs</groupId>
화사나 제작사 프로젝트 이름

<artifactId>Test</artifactId>
프로젝트에 할당된 고유이름

<name>Test</name>
보통 아티팩트ID와 동일함

<version>1.0.0-BUILD-SNAPSHOT</version>
프로그램 버전

<packaging>jar</packaging>
패키지 종류, jar, zip. web일경우 war.


<properties>
		<java-version>1.6</java-version>
		<org.springframework-version>5.2.15.RELEASE</org.springframework-version>
		<org.aspectj-version>1.6.10</org.aspectj-version>
		<org.slf4j-version>1.6.6</org.slf4j-version>
</properties>
이 pom.xml에서 사용하는 속성값 등을 모아둠. 필요에따라 바뀜


<dependencies> ...... 의존 라이브러리 정보 ...... </ dependencies>
의존 라리브러리. 이 프로그램이 참조하는 Java 기본 시스템을 제외한 라이브러리. 자동으로 기록되기때문에 편집하지않음.

<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-jdbc</artifactId>
	<version>${org.springframework-version}</version>
</dependency>
라이브러리 정보. 그룹ID, 아티팩트ID, 버전, 범위를 포함. <dependencies>태그안에 있어야한다.
이 정보들은 https://mvnrepository.com/ 여기서 검색한다(위 예시https://mvnrepository.com/artifact/org.springframework/spring-context/5.2.15.RELEASE)




