---
title: "TEST"
date: 2026-02-11T16:00:00+09:00
draft: false
math : true
tags: ["Math", "Statistics", "Python", "Tutoring"]
---

## 1. 수식은 현실 세계를 압축한 파일이다

최근 중고등학생들을 대상으로 수학과 과학 과외를 진행하며 가장 많이 하는 고민은, "어떻게 하면 학생들이 공식을 단순 암기하지 않고 직관적으로 이해하게 만들까?"이다.

사이버국방학과에서 시스템 보안을 공부하거나 알고리즘 트레이딩 모델을 설계할 때도 마찬가지다. 데이터의 흐름을 분석하고 논리적 오류를 방어하려면 통계학적 기초가 탄탄해야 한다. 오늘은 그중에서도 데이터 간의 관계를 설명하는 핵심 개념인 **공분산(Covariance)**과 **확률의 연속성(Continuity of Probabilities)**에 대해 내 생각을 정리해 둔다.

## 2. 공분산(Covariance): 두 변수는 어떻게 함께 움직이는가?

공분산은 두 확률변수 $X$와 $Y$가 어떤 양상으로 결합하여 변동하는지를 나타내는 지표다. 수식으로는 다음과 같이 정의된다.

$$Cov(X, Y) = E[(X - \mu_X)(Y - \mu_Y)]$$

여기서 $\mu_X$와 $\mu_Y$는 각각 $X$와 $Y$의 기댓값(평균)이다. 이 수식을 가만히 뜯어보면 아주 우아한 논리가 숨어있다.

* $X$가 자신의 평균보다 클 때(양수), $Y$도 자신의 평균보다 크면(양수), 두 값의 곱은 **양수(+)**가 된다.
* $X$가 평균보다 작을 때(음수), $Y$도 작으면(음수), 음수 곱하기 음수이므로 역시 **양수(+)**가 된다.

즉, 두 변수가 같은 방향으로 움직이는 경향이 있다면 공분산은 양수를 띠고, 반대 방향으로 움직인다면 음수를 띤다. 금융 데이터 분석에서 두 자산(예: 비트코인과 미국 주식)의 커플링 현상을 수치화할 때 가장 먼저 쓰이는 원리이기도 하다.

## 3. 확률의 연속성(Continuity of Probabilities)

해석학이나 고급 통계학으로 넘어가면 다루게 되는 '확률의 연속성' 개념도 매우 흥미롭다. 사건의 열(sequence of events) $A_1, A_2, \dots$ 이 단조증가(monotone increasing)할 때, 다음이 성립한다.

$$\lim_{n \to \infty} P(A_n) = P\left(\lim_{n \to \infty} A_n\right) = P\left(\bigcup_{n=1}^{\infty} A_n\right)$$

이 수식은 극한(Limit) 기호와 확률 척도(Probability Measure)의 연산 순서를 바꿀 수 있다는 것을 수학적으로 보장해 주는 강력한 정리다. 무한히 랜덤하게 오브젝트가 스폰되는 게임 로직이나, 무한 시행을 전제로 하는 트레이딩 모델을 설계할 때 백엔드 로직의 수학적 정당성을 부여해 준다.

## 4. Python으로 구현해 보는 Covariance

수학적 직관을 얻었다면, 코드로 검증해 볼 차례다. Python을 사용하면 복잡한 수식을 아주 간결하게 표현할 수 있다.

```python
import numpy as np

def calculate_covariance(x, y):
    """
    수식을 그대로 코드로 옮긴 표본 공분산 계산 함수
    """
    if len(x) != len(y):
        raise ValueError("두 데이터 세트의 크기가 같아야 합니다.")

    mean_x = np.mean(x)
    mean_y = np.mean(y)

    # E[(X - uX)(Y - uY)] 의 구현
    cov = np.sum((x - mean_x) * (y - mean_y)) / (len(x) - 1) 
    return cov

# 임의의 두 데이터 흐름 테스트
asset_A = np.array([10, 20, 30, 40, 50])
asset_B = np.array([12, 24, 33, 41, 58])

print(f"공분산: {calculate_covariance(asset_A, asset_B)}")