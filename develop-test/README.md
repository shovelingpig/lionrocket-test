# StarGAN v2 Code Practice

StarGAN v2 Official Implementation을 Custom한 소스코드의 Github 저장소 링크입니다.

[Minchan's Custom Implementation](https://github.com/shoveling-pig/custom-stargan-v2)

---

## Example Fake Images

저희 집 고양이 링가입니다. 아주 귀엽습니다.

<img src="/assets/result/linga.jpeg" width="300" height="300" />

저희 집 고양이 링가의 Identity에 검정색 강아지의 Domain과 Style을 합성해보았습니다.

<img src="/assets/result/linga_plus_dog.jpg" width="500" height="500" />

저희 집 고양이 링가의 Identity에 위엄있는 호랑이의 Domain과 Style을 합성해보았습니다.

<img src="/assets/result/linga_plus_wildlife.jpg" width="500" height="500" />

제가 자주 가는 카페에 걸려있는 귀여운 고양이 인간 그림입니다. 저희 집 고양이 링가와 저를 합성하면 과연 비슷한 모습이 나올지 궁금합니다.

<img src="/assets/result/cafe_cat_man.jpeg" width="500" height="500" />

제 어릴적 모습의 Identity에 저희 집 고양이 링가의 Domain과 Style을 합성해보았습니다. AFHQ 데이터셋으로만 학습된 모델이라 그런지 Visual Quality가 높지는 않지만 느낌은 그럴싸합니다.

<img src="/assets/result/baby_plus_linga.PNG" width="500" height="500" />

---

## Interpolation Videos

AFHQ 데이터셋을 학습한 모델을 활용해 생성한 이미지들입니다.

<img src="/assets/result/afhq_video.gif" />

CelebA-HQ 데이터셋을 학습한 모델을 활용해 생성한 이미지들입니다.

<img src="/assets/result/celeba_video.gif" />

---

## All Fake Images

<img src="/assets/result/afhq_result1.jpg" />

<img src="/assets/result/celeba_result2.jpg" />

---

## W&B Training Report

[Traning Report](https://wandb.ai/minchan/custom-stargan-v2/reports/Training-Report--Vmlldzo5ODI4NjQ?accessToken=827xwqlte3oee2en99n215davq9636zasm4y2l96g99sqz7wjn2rnaprw3m47sim)
