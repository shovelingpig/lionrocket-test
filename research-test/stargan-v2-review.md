# StarGAN v2 Review

## 요약
### 1. 배경: 문제를 제기하게 된 배경
MWGAN이나 StyleGAN 등 Style Diversity를 달성한 모델들은 단일 신경망으로 다중 도메인 간 I2I 변환을 할 수 없는 **Scalability**의 한계가 있었고, StarGAN 등 Scalability를 달성한 모델들은 항상 각 도메인당 동일한 Output을 생성하는 **Style Diversity**의 한계가 있었다. 

### 2. 문제: 저자가 해결하고자 하는 문제
다중 도메인으로 확장 가능할뿐만 아니라 다양한 스타일의 이미지를 생성할 수 있는 **Scalability와 Style Diversity를 모두 갖춘 신경망**을 만들자.

### 3. 해결방안: 문제 해결을 위해 도입한 방법론
임의의 Gaussian Noise를 Style code로 변환하는 과정을 학습하는 **Mapping Network**와 주어진 Reference Image에서 Style Code를 추출하는 과정을 학습하는 **Style Encoder**를 활용하여, 기존의 고정된 Domain Label을 다양한 스타일을 표현할 수 있는 Domain-specific **Style Code**로 대체한다.

### 4. 근거: 해결방안을 도입한 근거
- Adversarial Loss: Generator가 더 진짜같은 이미지를 생성하도록 하는 Loss 
- Style Reconstruction Loss: Generator가 이미지 생성에 Style을 활용하도록 강제하는 Loss
- Style Diversification Loss: Generator가 더 다양한 Style의 이미지를 생성하도록 Image Space를 돌아다니게 만드는 Loss
- Cycle Consistency Loss: Generator가 이미지의 Identity는 자체는 보존하도록 하는 Loss

### 5. 기여점: 이전까지 논문들과의 차이점, 기여점, 개선사항
StarGAN v2는 Celeb-HQ 데이터셋과 AFHQ 데이터셋에 대한 정량적인 평가(FID, LPIPS)와 정성적인 평가(AMT) 결과, 기존의 다른 모델들보다 **생성된 이미지의 질(Visual Quality)**, **스타일의 다양성(Diversity)**, **다중 도메인으로의 확장 가능성(Scalability)** 측면에서 상대적으로 성능이 우수하다.

---

## 한계
- 학습 속도가 느리다.(100K iteration, 3 days on a single Tesla V100 GPU)
- 기존보다 더 다양한 스타일의 분포를 학습하긴 하지만, 여전히 모든 스타일에 대한 전체적인 분포는 학습하지는 못한다.
- Style Diversification Loss의 목적함수는 최적화 지점이 없기 때문에 선형적으로 Weight를 0으로 줄여가며 학습(Decaying)해야 한다.

---

## 궁금한 점
- StarGAN v2에 MMW Distance(Multi-marginal Wasserstein Distance)를 적용할 수는 없을까?
- FID와 LPIPS가 각각 Visual Quality와 Diversity를 평가하기에 가장 적절한 지표일까?
- Reference Image를 이용한 이미지 합성을 통해 만들 수 있는 성형, 미용, 패션, 예술 등의 분야의 재밌는 프로덕트는 없을까? (예를 들어 고객이 자신이 좋아하는 연예인의 사진을 Reference Image로 입력하면 특정 부위 성형 후 고객의 얼굴을 생성해주는 모델을 만들 수는 없을까?) 
- Style/Domain/Identity의 정의가 애매하지 않나?
- 이미지 속 다양한 Attribute 집합의 Combination 중에서 특정 Combination을 선택하여 각각을 Style, Domain, Identity로 설정할 수는 없을까?
- 선택적인 데이터 라벨링을 통해서만 이러한 구분을 설정할 수 있는 걸까? 모델링 구조를 통해서 이러한 구분을 하이퍼파라미터로 더 유연하게 설정할수는 없을까? (예를 들어 특정 연예인의 코로 성형한 내 모습을 보고 싶으면 코의 모양만을 Identity에서 제외시키고 Style로 포함시킬 수는 없을까?)
---