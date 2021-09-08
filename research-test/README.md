# StarGAN v2 Review

## 요약
### 1. 배경
StyleGAN 등 Style Diversity를 달성한 모델들은 단일 신경망으로 다중 도메인 간 I2I 변환을 할 수 없는 **Scalability**의 한계가 있었고, StarGAN 등 Scalability를 달성한 모델들은 항상 각 도메인당 동일한 Output을 생성하는 **Style Diversity**의 한계가 있었다. 

### 2. 저자가 해결하고자 하는 문제
다중 도메인으로 확장 가능할뿐만 아니라 다양한 스타일의 이미지를 생성할 수 있는 **Scalability와 Style Diversity를 모두 갖춘 신경망**을 만들자.

### 3. 문제 해결을 위해 도입한 방법론
임의의 Gaussian Noise를 Style code로 변환하는 과정을 학습하는 **Mapping Network**와 주어진 Reference Image에서 Style Code를 추출하는 과정을 학습하는 **Style Encoder**를 활용하여, 기존의 고정된 Domain Label을 다양한 스타일을 표현할 수 있는 **Domain-specific Style Code**로 대체한다.

### 4. 해결방안을 도입한 근거
- **Adversarial Loss**: Generator가 더 진짜같은 이미지를 생성하도록 하는 Loss 
- **Style Reconstruction Loss**: Generator가 이미지 생성에 Style Code를 활용하도록 강제하는 Loss
- **Style Diversification Loss**: Generator가 더 다양한 Style의 이미지를 생성하도록 Image Space를 돌아다니게 만드는 Loss
- **Cycle Consistency Loss**: Generator가 이미지의 Identity는 자체는 보존하도록 하는 Loss

### 5. 이전 논문들과의 차이점
StarGAN v2는 Celeb-HQ 데이터셋과 AFHQ 데이터셋에 대한 정량적인 평가(FID, LPIPS)와 정성적인 평가(AMT) 결과, 기존의 다른 모델들보다 **생성된 이미지의 질(Visual Quality)**, **스타일의 다양성(Diversity)**, **다중 도메인으로의 확장 가능성(Scalability)** 측면에서 상대적으로 성능이 우수하다.

---

## 한계
* 학습 속도가 느리다. (8 Batch, 100K iteration, 3 days on a single Tesla V100 GPU)
* 기존보다 더 다양한 스타일의 분포를 학습하긴 하지만 여전히 모든 스타일에 대한 전체적인 분포는 학습하지는 못한다.
* MWGAN과 달리 Inter-domain Loss를 적용하고 있지 않기 때문에 여러 도메인 간의 복잡한 관계를 학습하지 못하여, Target Domain에서 생성된 이미지들의 분포가 MWGAN에 비해 Real Distribution에 상대적으로 덜 가깝습니다.
---

## 궁금한 점
* StarGAN v2에 MWGAN의 MMW Distance(Multi-marginal Wasserstein Distance)를 적용해볼 수는 없을까?
* FID와 LPIPS가 각각 Visual Quality와 Diversity를 평가하기에 가장 적절한 지표일까?
* 어떤 논리와 근거로 논문의 저자들은 Domain-specific Style Code가 Domain-shared Style Code보다 더 Output Diversity가 높다고 주장하고 있는 걸까?
* 미용, 성형, 패션, 예술 등의 분야에서 Reference-guided 이미지 합성을 통해 만들 수 있는 상용화 가능성이 있는 프로덕트는 없을까?
> 예를 들어 미용 분야에서는 고객이 원하는 헤어스타일의 인물 사진을 Reference Image로 입력하면 그 헤어스타일을 한 고객의 모습을 생성해주는 모델을 만들 수 있다. 또 성형 분야에서는 고객이 자신이 좋아하는 연예인의 사진을 Reference Image로 입력하면 고객 얼굴의 특정 부분을 해당 연예인처럼 성형한 후의 추정 얼굴을 생성해주는 모델을 만들 수도 있다. 패션 분야에서는 유명 디자이너가 만든 가방 사진을 Reference Image로 입력하면 비슷한 스타일의 지갑 디자인을 생성해주는 모델도 생각해볼 수 있다. 또는 고객이 원하는 스타일의 의상을 선택하면 해당 의상을 착용한 고객의 모습을 생성해주는 가상 피팅 서비스도 만들 수 있다.
* 본 논문에서 정의하고 있는 Style과 Identity의 정의에 모호한 측면이 있다. 더 수학적으로 엄밀히 정의할 수는 없을까?
> 내 생각은 다음과 같다. Domain은 시각적으로 구분할 수 있는 하나의 카테고리로 묶일 수 있는 이미지들의 집합이다. Domain을 시각적으로 구분할 수 있도록 하는 특징들을 Domain의 Feature Set이라고 하자. Identity는 학습 과정에서 Cycle Consistency Loss를 통해 보존되는 Feature Set이다. Cycle Consistency Loss를 학습에 적용하는 방식에 따라 Identity를 유동적으로 변경할 수 있다. Style은 특정 이미지의 전체 Feature Set에서 Identity와 Domain의 Feature Set을 제외한 차집합이다. 따라서 Domain과 Identity를 어떻게 설정하느냐에 따라서 Style의 범위 또한 바뀐다. 마지막으로 Domain-specific Style Code란 Style에 Domain의 Feature Set에 대한 정보를 합한 벡터이다. 
* 이미지 속 다양한 Feature들의 Combination 중에서 특정 Combination을 선택하여 각각을 Style, Domain, Identity로 설정할 수는 없을까?
* Self-supervised Learning에서 사진의 일부를 Masking하는 방법을 응용하여 Cycle Consistency Loss를 특정 Feature Set에만 적용시키지 않는 방법은 없을까? 또는 데이터 전처리가 아닌 모델링 구조를 통해서 이러한 Style Identity의 구분을 하이퍼파라미터로 조금 더 유연하게 설정할 수는 없을까?
> 예를 들어 특정 연예인의 코로 성형한 내 모습을 보고 싶으면 코의 모양만을 Identity에서 제외시키고 Style로 포함시킬 수는 없을까?
---
