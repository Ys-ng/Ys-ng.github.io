---
layout: post
title: PKI (Public Key Infrastructure)인증서와 해쉬
subtitle: blockchain encryption
categories: BlockChain
tags: [encryption, blockchain]
---



이산대수암호(비대칭키암호) 
엘가말 암호는 이산대수(離散對數) 문제에 대한 최초의 공용 키 암호이며 DH 공용 키 분배법의 확정형이다. 이산대수 문제의 어려움이란, 주어진 g, x, p를 이용하여 y = g^x mod p를 구하긴 쉽지만, g, y, p 값을 이용하여 원래의 x는 찾기 어렵다는 것이다.

> ### PKI 
> ( Public Key Infrastructure)인증서
> 공개 키 기반' , 또는 '공개 키 인프라' 라고 해석할 수가 있다
> PKI 기반을 이해할려면 3가지 기본적으로 알고 있어야 하는것들 
* 해쉬함수 (Message Digest) Computer Science 에서 부르는 Hash 는 Data Structure 에서 쓰이는 형식을 의미 하기 때문에 보안쪽에서 쓰이는 '해쉬 함수'는 Cryptographic Hash Function 이라고 구별해서 부름)
* 대칭키 (Symmetric Key Algorithm)
* 비 대칭키 (Asymmetric Key Algorithm)

### 해쉬
임의크기입력 -> 고정크기의 유일한 출력      유일-> "무결성"(기밀성, 무결성, 
* 빠른연산을 제공해야한다
* 충돌회피

특징
* 단방향성을 가진다(해쉬값으로 원본을 찾을수 없다)
a -> H(a)        O
a <- H(a)        X


대칭에비해서 비대칭은 1000배 느리다?






무결성
데이터가 바뀐것을 무결하다하고 한다. ABCD를 바꿀수있는 사람이 있고 절차가 있지만 그걸 무시하고 바꾼것을 변조라 한다.
그 절차대로 바뀐것을 증명하는것이 무결하다 한다. 

단방향성=> "인증"
- 식별                           ->id
- 인증(Authentication)      ->password 
	인증 방식 (지식기반, 소유, 일반적/신체적/서명 특징)
- 인가 (Authorization) 



사용자가 패스워드를 생성함 -> DB에 저장 -> 제3자가 가져갈수있다



salt
해쉬가 크랙킹되는것을 방어하는것






