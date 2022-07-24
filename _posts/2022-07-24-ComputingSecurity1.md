---
title: "컴퓨팅보안 -1"
categories: Security
tags: [보안, security]
comments: true
toc: true
author_profile: true
sidebar:
  nav: "docs"
---
### 개념 정리

---

- 양자 컴퓨터(Quantum Computer) : 얽힘(entanglement)이나 중첩(superposition) 같은 양자역학적인 현상을 활용하여 자료를 처리하는 계산 기계이다. 또한 그러한 방법을 '양자 컴퓨팅'(quantum computing)이라고도 한다.고전적인(전통적인) 컴퓨터에서 자료의 양은 비트로 측정되는 것에 비해, 양자 컴퓨터에서 자료의 양은 큐비트로 측정된다. 양자 정보 통신을 활용한 양자 컴퓨터는 한 개의 처리 장치에서 여러 계산을 동시에 처리할 수 있어 정보처리량과 속도가 지금까지의 컴퓨터에 비해 뛰어나다.
- 양자 암호(Quantum cryptography) : 양자 역학적 특성을 활용한 암호 작업을 수행하는 과학. 양자 컴퓨터로 인해 키 교환 방식 문제를 해결하기 위해 제안된 Quantum key distribution 이 대표적인 Quantum cryptography 의 예시가 됨

### 컴퓨팅보안 개요

---

- Symmetric & Asymmetric Foundations
    
    암호화 방식은 크게 동기화, 비동기화 방식으로 나눌 수 있다. 암호화 강도를 높이기 위해서는 혼돈과 확산 성질을 이용해야 한다.
    
    - 혼돈(Confussion)과 확산(Diffusion)
        - 혼돈 : 암호문의 통계적 성질과 평문의 통계적 성질의 관계를 난해하게 만드는 성질
        - 확산 : 평문 비트와 키 비트가 암호문의 모든 비트에 영향을 주는 성질
    - 대칭 암호화 방식 : SEED, DES, AES 등의 알고리즘이 있음
    - 비대칭 암호화 방식 : 대칭 암호화의 암호화 키 전달 문제를 해결하기 위한 목적
    - 대표적인 비대칭 암호화 방식 : RSA
    - Https로 살펴보는 암호화 방식
        - 비대칭 암호화는 대칭 암호화에 비해 느리다는 단점이 있다.
        - 비대칭 암호화는 Client와 서버가 handshake를 할 때, 대칭 암호화는 이후 통신을 할 때 사용한다.
- Hash
    - 해시는 정보를 숨기는 암호화와는 달리, 변조를 확인 하는 것, 다시 말해 정보의 무결성을 확인하기 위해 사용된다.
    - MD5의 경우 16^32 의 값으로 결과를 표현할 수 있지만 무한이 아니므로 서로 다른 값이 동일한 해시값을 가질 수 있다. 이것을 Collision 이라고 한다.
    - Collision의 발생 가능성이 클 수록 취약하다고 한다.
    - 해시는 복호화가 불가능 하며 이러한  성질을 일방향성 이라고 한다.
    - 해시 알고리즘에는 MD, SHA 등이 있다.
- Cryptocurrency & Block Chain
    - 개념의 크기로 비교하였을 때 Block chain > Cryptocurrency > Bitcoin으로 표현 할 수 있다.
    - Bitcoin은 사토시 나카모토가 만들었으며, 화폐의 Decentralization을 목표로 만들어 졌다.
    - Ethereum은 Bitcoin과 달리smart contract를 사용한다.

### Information Security

---

보안은 Confidentiality, Integrity, Availability 속성으로 집약된다.

- Confidentiality(기밀성) : 인가된 사용자만 정보 자산에 접근할 수 있는 성질
- Integrity(무결성) : 권한을 가진 사용자가 인가한 방법으로만 정보를 변경할 수 있도록 하는 성질
    - Blockchain 이 Integrity를 보장하는 대표적인 기술이다.
- Availability(가용성) : 필요한 시점에 정보 자산에 대한 접근이 가능하도록 하는 성질
    - DDos 공격은 Availability를 해치는 대표적인 예시이다.

### 암호와 보안 기술의 변화

---

시대별 주목받은 주목받는 보안 기술이 변하였.

- 통신 보안 → 컴퓨터 보안 → 네트워크 보안 → 인터넷 보안 → 유비쿼터스 보안
    - 사이버 보안은 전 세대에 포괄하여 다루어지고 있다.
    

### 한국의 정보보호 연혁

---

1964년 부터 현재에 이르기 까지 보안 관련 다양한 발전을 이루어 왔다.