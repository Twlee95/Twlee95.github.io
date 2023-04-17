---
title:  "[논문리뷰/공부] Stable diffusion"
excerpt: "뭐지"

categories: [AI, 논문리뷰/공부]
tags:
  - [AI, 논문리뷰, 공부, Generative Model, Stable Diffusion, Latent Diffusion]

toc: true
toc_sticky: true
 
date: 2023-04-17
last_modified_at: 2023-04-17
---

## Stable Diffusion

지금부터 Stable Diffusion의 개요와 세부적인 모델 구조에 관하여 알아보겠다 !


#### Stable Diffusion이란

diffusion은 이미지 생성모델 중 하나임.
Autoencoder, GAN, Diffusion이 대표적인 생성모델이다.

Autoencoder는 다양한 이미지를 생성가능하지만 품질이 낮다는 담점이 있다.
GAN은 이미지 품질은 상대적으로 뛰어나지만 다양한 이미지를 생성하는데 어려움을 겪는다.
하지만, Diffusion은 다양하고 품질이 높은 이미지를 생성가능하게 한다.

#### Stable diffusion의 원리는 무엇일까
Diffusion Model은 기본이미지(시간 t=0)에 chatGPT가 노이즈(랜덤한 색상의 점)을 추가함
이 과정을 1000번 정도 반복하면 우측과 같이 순수한 노이즈와 유사한 이미지로 변환이 된다.
이렇게 만들어진 예시가 openAI의 DALL-E2 모델이다.
![Diffusion Model](https://user-images.githubusercontent.com/76574427/232390055-5a20cf25-c86b-4708-b8b9-b5530437228a.png)

초기에는 낮은 품질을 보이다가 점차 높은 품질로 수렴하게 된다.



#### Diffusion Model의 단점...?
이렇게 완벽하게 보이는 Diffusion Model에도 단점이 있었는데,
매우 많은 픽셀을 1000번 이상 반복하는 것은 컴퓨팅 능력이 매우 많이 필요한 작업이다.

그래서 이를 해결하기 위해 새로운 방법인 Latent Diffusion Model이 등장했다!
Latent Diffusion Model은 이미지 학습을 위한 첫 단계에서 VAE(Variational Autoencder)나 U-Net과 같은 인코딩 방법을 사용하여 이미지를 변환합니다.
이렇게 인코딩된 이미지는 잠재 변수로서 압축된 행렬로 표현됩니다.

![Image to latent space](https://user-images.githubusercontent.com/76574427/232394460-842f3139-a91a-4f03-a7c7-0f67e9cdb379.png)

이렇게 압축된 행렬에 노이츠를 추가하고 복구함으로써
기존 Diffusion에 비해 학습 속도가 매우 개선된다.

![Procedure of Stable Diffusion](https://user-images.githubusercontent.com/76574427/232398645-4659c342-bdc0-495a-8835-5856b0313c6e.png)

Latent Sapce를 활용하여 Diffusion이 진행되는데 이를 Stable diffusion 이라고 한다.




#### 구체적인 Stable Diffusion의 구조










