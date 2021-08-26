# StarGAN v2 Review

## 요약
### 1. 배경: 문제를 제기하게 된 배경
MWGAN이나 StyleGAN 등 Style Diversity를 달성한 모델들은 단일 신경망으로 다중 도메인 간 I2I 변환을 할 수 없는 **Scalability**의 한계가 있고, StarGAN 등 Scalability를 달성한 모델들은 항상 각 도메인당 동일한 Output을 생성하는 **Style Diversity**의 한계가 있다. 

### 2. 문제: 저자가 해결하고자 하는 문제
다중 도메인으로 확장 가능할뿐만 아니라 다양한 스타일의 이미지를 생성할 수 있는 **Scalability와 Style Diversity를 모두 갖춘 신경망**을 만들자.

### 3. 해결방안: 문제 해결을 위해 도입한 방법론
임의의 Gaussian Noise를 스타일 코드로 변환하는 과정을 학습하는 **Mapping Network**와 주어진 Reference Image에서 스타일 코드를 추출하는 과정을 학습하는 **Style Encoder**를 활용하여, 기존의 Domain Label을 다양한 스타일을 표현할 수 있는 Domain-specific **Style Code**로 대체한다.

### 4. 근거: 해결방안을 도입한 근거
- Adversarial Loss
- Style Reconstruction Loss
- Style Diversification Loss
- Cycle Consistency Loss
- Total Loss

### 5. 기여점: 이전까지 논문들과의 차이점, 기여점, 개선사항
StarGAN v2는 Celeb-HQ 데이터셋과 AFHQ 데이터셋에 대한 정량적인 평가(FID, LPIPS)와 정성적인 평가(AMT) 결과, 기존의 다른 모델들보다 **생성된 이미지의 질(Visual Quality)**, **스타일의 다양성(Diversity)**, **다중 도메인으로의 확장 가능성(Scalability)** 측면에서 상대적으로 성능이 우수하다.

---

## 한계
- 학습 속도가 느리다.
- 여전히 모든 스타일에 대한 전체적인 분포는 학습하지는 못한다.
- Style Diversification Loss의 목적함수는 최적화 지점이 없기 때문에 선형적으로 Weight를 0으로 줄여가며 학습(Decaying)해야 한다.

---

## 궁금한 점
- StarGAN v2에 MMW Distance(Multi-marginal Wasserstein Distance)를 적용할 수는 없을까?
- 학습이 끝난 뒤 Style Diversity가 잘 달성되었는지 평가할 수 있는 더 좋은 지표는 없을까?
- Style Diversification Loss에 대해서 선형적으로 Weight를 0으로 줄이며 학습(Decaying)하는 것보다 더 좋은 방법은 없을까?
- Reference Image를 이용한 이미지 합성을 통해 만들 수 있는 재밌는 프로덕트는 없을까?

---