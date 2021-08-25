# StarGAN v2 Review
---

## Abstract
1. 배경: 문제를 제기하게 된 배경
기존의 Star GAN은 1개의 Generator로 Multi Domain I2I Translation을 가능하게 만들어 Scalability의 한계를 극복했지만 여전히 Style Diversity의 한계를 가지고 있었다. 여기서 Style Diversity란 데이터 분포에 대한 다양한 특성을 반영하는 정도를 의미한다. 즉, Star GAN은 각 도메인당 결정론적 매핑을 학습할 뿐 데이터 분포의 다중 모델 특성을 포착하지는 못했다. 이는 각 도메인이 미리 정해진 라벨로 표시된다는 점에서 비롯되었다. Star GAN에서 Generator는 one hot vector로 된 고정 라벨을 입력받고, 따라서 소스 이미지에 따라 불가피하게 각 도메인당 동일한 Output을 생성한다.

2. 문제: 저자가 해결하고자 하는 문제
Scalability뿐만 아니라 Style Diversity도 높은 신경망을 만들고자 했다.

3. 해결방안: 문제 해결을 위해 도입한 방법론
기존의 도메인 라벨을 특정 도메인의 다양한 스타일을 표현할 수 있는 도메인별 스타일 코드로 대체했다. 스타일 코드를 활용하는데는 Mapping Network와 Style Encoder를 사용했다.
- Mapping Network : 임의의 가우스 노이즈를 스타일 코드로 변환하는 과정을 학습
- Style Encoder: 주어진 소스 이미지에서 스타일 코드를 추출하는 과정을 학습

4. 근거: 해결방안을 도입한 계기, 근거

5. 기여점: 이전까지 논문들과의 차이점, 기여점, 개선사항
스타일 코드를 이용하여 Generator가 여러 도메인에 걸쳐 다양한 이미지를 합성하는 과정을 학습한다.

---

## 한계
---

## 궁금한 점
---