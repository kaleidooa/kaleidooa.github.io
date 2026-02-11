---
title: "포트폴리오 겸 블로그 구축을 시작하며"
date: 2026-02-11T15:00:00+09:00
draft: false
tags: ["DevLog", "Hugo"]
---

단순히 완성된 코드를 나열하는 것을 넘어, 치열하게 고민했던 과정과 논리의 흐름을 기록하기 위해 Hugo 기반의 블로그를 구축했다. 

앞으로는 이곳에 시스템 아키텍처, 파이썬을 활용한 금융 데이터 분석 로직, 그리고 게임 엔진의 코어 로직을 구현하며 겪었던 트러블슈팅 과정을 정리할 예정이다.

## 테스트 1: 코드 블록 삽입
투자 비중을 계산하는 로직의 일부를 파이썬 코드로 정리해보았다.
```python
def calculate_kelly_criterion(win_rate, reward_to_risk_ratio):
    """
    승률과 손익비를 바탕으로 켈리 공식에 따른 최적 투자 비중 계산
    """
    f_star = (win_rate * reward_to_risk_ratio - (1 - win_rate)) / reward_to_risk_ratio
    return f_stars