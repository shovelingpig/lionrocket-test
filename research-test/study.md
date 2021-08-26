# GAN
Implicit Density Function  
Generator와 Discriminator의 적대적 관계를 이용한 Min Max Game  

# ConditionalGAN
조건을 함께 입력  

# Pix2Pix
Image-to-Image Translation  
Image를 Condition으로 입력한다.  

# CycleGAN
이미지의 Content를 유지하기 위해 Generator G와 Inverse Function F를 함께 학습시킨다.  

# WGAN
Critic Loss  
Weight Clipping을 이용하여 제약조건을 만족하도록 한다.  

# WGAN-GP
Critic Loss + Gradient Penalty  

# StarGAN
Adversarial Loss + Domain Classification Loss + Reconstruction Loss  
하나의 신경망을 활용해서 다중 도메인 사이에서의 이미지 변환을 가능하게 한다.  

# Start AN v2
I2I는 두 개의 다른 비주얼 도메인 간의 매핑(변환)을 학습하는 것이 목표  
도메인이란 시각적으로 구분되는 이미지의 집합


## Reference
[Official Paper](https://arxiv.org/abs/1912.01865)  
[Official Implementation](https://github.com/clovaai/stargan-v2)  
[Other Implementations](https://paperswithcode.com/paper/stargan-v2-diverse-image-synthesis-for)  
[Related Article 1](https://kozistr.tech/StarGANv2/)  
[Related Article 2](https://comlini8-8.tistory.com/13)  
[Related Article 3](https://medium.com/curg/stargan-v2-%ED%95%98%EB%82%98%EC%9D%98-%EB%AA%A8%EB%8D%B8%EB%A1%9C-%EC%97%AC%EB%9F%AC-%EC%8A%A4%ED%83%80%EC%9D%BC%EC%9D%98-%EC%9D%B4%EB%AF%B8%EC%A7%80%EB%A5%BC-%EC%83%9D%EC%84%B1%ED%95%9C%EB%8B%A4-acdfb0ac822a)  
[Related Videos](https://www.youtube.com/results?search_query=stargan+v2)  