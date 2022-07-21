---
title: "AI - Few shot learning replication"
categories: AI
tags: [AI, Few shot learning, Deep learning]
comments: true
toc: true
author_profile: true
sidebar:
  nav: "docs"
---

## Motivation

Classification 모델을 사용하기 위해서는 일반적으로 충분히 많은 데이터가 필요하지만 실제 생활이나 산업에는 충분한 데이터를 확보하기 어렵다. 최근 Few shot Classification은 어러 문제를 해결하는 방법으로 거론되고 있다. Few shot classification 성능향상을 위한 Smoother Manifold를 적용한 모델을 적용하고 실용성을 확인해 보고자 한다.

![image info](/assets/9977b765c595435a96191cd8fdd4be39/Untitled.png)

## Goal

1. ECCV2020에 발표된 논문 Replication

   [Embedding Propagation: Smoother Manifold for Few-Shot Classification](https://arxiv.org/abs/2003.04151)

2. 자체 데이터를 이용한 실험

## Background

### Few-shot learning

- 제한된 적은 수의 Sample을 이용하여 예측 진행
- Supervised Learning vs. Few-shot Learning
  - Supervised Learning
    - Training set이 큼
    - Test sample이 Known class 여야 함
  - Few-shot learning
    - Support set이 작음
    - Query samples가 Unknown class 여도 됨
  
![image info](/assets/9977b765c595435a96191cd8fdd4be39/Untitled%201.png)

### EPNet(Embedding Propagation Netwrok)

- 같은 클래스의 노드는 서로 가까운 거리에 위치하도록 학습이 진행됨
- Feature vector가 구해지면 클래스를 구분할 수 있는 경계가 정해짐
- EPNet의 경우 이 경계를 부드럽게 하여 정확도를 높이게 됨
- 아래 회색 마름모의 경우 경계를 부드럽게 하지 않으면 원형의 클래스로 예측되지만, 경계를 부드럽게 함으로써 원래의 마름모 클래스로 예측함

![image info](/assets/9977b765c595435a96191cd8fdd4be39/Untitled%202.png)

### EPNet Training Procedure

크게 아래 두 과정으로 진행

1. Pretraining Phase
   - Embedding propagation을 이용하여 Classification loss와 Rotation loss를 낮추는 방식으로 학습 진행
   - 클래스의 일반적인 특증을 표현할 수 있도록 학습 진행
2. Episodic fine-tuning
   - Pretraining에서 사용했던 데이터 일부를 가져와 Support set을 생성
   - Support set과 Query set을 이용하여 Classification loss와 Label propagation loss를 최소화하는 Fine-tuning 진행

![image info](/assets/9977b765c595435a96191cd8fdd4be39/Untitled%203.png)

### Semi supervised learning

- supervised learning과 unsupervised learning의 중간 단계로 레이블이 있는 데이터가 적고 레이블이 없는 데이터를 함께 가지고 있을 때 유용함
- label이 없는 데이터를 활용하여 Decision boundary를 더 나은 성능이 보장되도록 설정

![image info](/assets/9977b765c595435a96191cd8fdd4be39/Untitled%204.png)

## 실험

프로젝트의 주 목적인 EPNet Replication 중 실험 시간과 환경을 고려하여 가능한 실험범위를 축소 정의하여 진행

### 실험 범위

- Method of Few shot classification : EPNet
- Backbone :CONV-4, RESNET12
- Dataset :miniImagenet
- Shots : 1-Shot, 5-Shot
- SSL(Semi-Supervised Learning) 추가 실험

![image info](/assets/9977b765c595435a96191cd8fdd4be39/Untitled%205.png)

## 실험

- Hyper parameter를 변경하며 1 Shot(파란선), 5 Shot(녹색선)에 대한 실험 진행
- 설정한 Parameter와 결과가 오차범위 내 일치하는 것을 확인

       (해당 논문의 Source code를 제공하는 github 참고)

[https://github.com/ElementAI/embedding-propagation](https://github.com/ElementAI/embedding-propagation)

- SSL의 경우 정확도가 논문결과와 비슷하지만 1 ~2% 정도 정확도가 낮게 나옴
  - SSL 실험이 단일 Hyper parameter로 진행되지 않은 것으로 판단됨

**CONV-4**

![image info](/assets/9977b765c595435a96191cd8fdd4be39/Untitled%206.png)

**Resnet12**

![image info](/assets/9977b765c595435a96191cd8fdd4be39/Untitled%207.png)

**SSL**

![image info](/assets/9977b765c595435a96191cd8fdd4be39/Untitled%208.png)

## 추가 실험

- EPNet의 실용성을 확인하기 위해 자체 데이터로 추가 실험 진행

**차량 모델 분류 실험 (5shot - 5way 실험)**

- 26.2%로 실용성 없음

![image info](/assets/9977b765c595435a96191cd8fdd4be39/Untitled%209.png)

**가전 제품 이미지 분류 실험 (5shot - 5way 실험)**

- 46.6%로 자동차 모델 분류 보다는 성능이 좋았지만 실용성 부족

![image info](/assets/9977b765c595435a96191cd8fdd4be39/Untitled%2010.png)

**공정 조립 모델 실험 (5shot - 4way 실험)**

- 95.19%로 자동차 모델, 가전제품 분류 모델에 비해 나은 정확도를 보임
- 조립 공정의 경우 이미지의 변경이 적고, 특징이 뚜렸하기 때문에 높은 정확도를 가져옴

![image info](/assets/9977b765c595435a96191cd8fdd4be39/Untitled%2011.png)

### 결론

- 논문 Replication 진행 및 EPNet 성능 확인
- **Few shot learning 시 Support set과 Query set의 특징이 뚜렸하고 변경사항이 없다면 적은양의 자체데이터로 높은 정확성을 가지는 분류를 진행할 수 있음**

**참고자료**

[1] Baseline Paper ([https://arxiv.org/abs/2003.04151](https://arxiv.org/abs/2003.04151))

[2] Few shot learning 참고 ([https://github.com/wangshusen/DeepLearning](https://github.com/wangshusen/DeepLearning))

[3] Few shot learning 참고 ([http://tlublog.com/posts/few-shot](http://tlublog.com/posts/few-shot))

[4] Semi-supervised learning 참고 ([https://blog.est.ai/2020/11/ssl/](https://blog.est.ai/2020/11/ssl/))
