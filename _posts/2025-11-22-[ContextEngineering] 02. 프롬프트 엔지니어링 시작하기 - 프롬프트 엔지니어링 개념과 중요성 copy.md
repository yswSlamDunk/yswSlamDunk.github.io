---
layout : single
title : "[ContextEngineering] 02. 프롬프트 엔지니어링 시작하기 - 프롬프트 엔지니어링 개념과 중요성"
categories : [PromptEngineering, LLM]
tag : [컨텍스트 엔지니어링, 프롬프트 엔지니어링, 프롬프트 엔지니어링 개념과 중요성, 강수진 박사의 프롬프트·컨텍스트 엔지니어링 아카데미]
---

## 프롬프트 엔지니어링 개념과 중요성
### 01. 프롬프트 엔지니어링 개념과 기술의 중요성

#### Prompt Engineering is still important
* 모델마다 민감하게 여기는 단어와 품사가 다르며, 특히 proprietary vs open-source llm 사이에서 간극이 두드러지게 나타남
  * 관련 논문: which words matter most in zero-shot prompts(https://arxiv.org/abs/2502.03418)
사용하는 llm 종류에 따라 적용해야 할 디테일이 prompt engineering 차원에서 달라짐

#### which words matter most in zero-shot prompts에서의 findings
* 작업별 단어 계층(Task-specific word hierarchies) 상이
  * 수학 문제에서는 "step-by-step"
  * 추론 문제에서는 "think"가 더 중요함
* 독점(proprietary) 모델이 오픈소스보다 인간 직관에 더 잘 부합
* 명사(nouns)가 더 중요
* 단어 중요도와 모델 성능의 역상관 관계
  * 모델 성능이 낮을수록(즉 모델이 어려워하는 작업일수록) 프롬프트 단어와 기호의 중요도가 더 커짐

### 02. 프롬프트 엔지니어링 서식과 표현에 대한 민감도
#### 프롬프트 엔지니어링이 까다롭고 어려운 까닭
1. 표현과 서식에 대한 민감도
2. 예시와 샘플 순서의 민감도
3. 재서술 말투 변화에 의한 성능 분산
4. 모델 평가의 어려움

#### 표현과 서식에 대한 민감도
* 프롬프트 서식(공백, 구두점, 헤더 등)만 바꿔도 성능이 최대 76% 변화(sensitivity)
  * quantifying language models' sensitivity to spurious features in pormpt design or: how i learned to start worrying about prompt formatiing(https://arxiv.org/abs/2310.11324)
  * 프롬프트 포멧 템플릿을 약간만 변경해도 동일한 작업에서 모델의 성능이 크게 달라질 수 있음
  * 오픈소스 llm (크기가 작으면 민감도 높음)들이 few-shot 설정에서 프롬프트 포맷의 미세한 변화에 극도로 민감하게 반응함을 발견
* 템플릿(json/markdown/yaml 등) 간 성능 편차 큼
  * does prompt formatting have any impact on llm performance(https://arxiv.org/abs/2411.10541)
  * 평문, markdown, json, yaml 등 사람이 읽기 쉬운 다양한 템플릿으로 변환
  * 고정된 프롬프트 템플릿 사용 방식 재고 필요 시사

### 03. 예시 샘플의 순서 민감도
#### 예시와 샘플 순서의 민감도
* fantastically ordered prompts and where to find them: overcoming few-shot prompt order sensitivity(https://arxiv.org/abs/2104.08786)
* 제공하는 예시의 순서에 따라 결과가 극적으로 달라짐을 보여주는 연구
  * 모델 크기와 무관하게(가장 큰 최신 모델에서도) 관찰됨
  * 특정 샘플 집합에만 해당하는 현상이 아님
  * 모델별 좋은 순열이 다름
* the few-shot dilemma: over-prompting large language models(https://arxiv.org/abs/2509.13196)
  * 예시 순서 변화가 성능을 무작위 추정 수준까지 떨어뜨릴 수 있음
  * 예시가 앞/뒤 위치에 있을 때 성능 차이 있음(앞에 적은 것이 영향 높음)
    * 동그라미 3개와 세모 2개의 예시를 작성했다고 가정
    * 앞에 먼저 작성한 3개의 동그라미 영향으로, 동그라미만 출력되는 경향이 있음

### 04. 재서술 말투 변화에 대한 성능 분산
* paraphrase types elicit prompt engineering capabilities(https://arxiv.org/abs/2406.19898)
* 프롬프트를 다양한 방식으로 바꿔(paraphrase) 언어적 특징들이 모델에 어떤 영향을 미치는지 체계적, 실증적으로 평가
* 다양한 위치에 적용된 언어적 변화(형태론, 구문, 어휘, 어휘+구문, 담화, 기타 등 6가지 패밀리) 를 통해 120개 과제에서 5가지 모델의 행동 변화를 측정
* 특정 유형의 패러프레이즈(예: 형태, 어휘 변화)에 맞게 프롬프트를 조정하면 모델 성능이 개선될 가능성이 있음

### 05. 모델 성능 평가의 어려움
* 민감성&비일관성: 프롬프트 변형에 대한 과도한 민감도. 아주 작은 문장 구조나 단어 변화가 결과를 뒤바꿀 수 있음(flaw or artifact)
* 평가 기준 모호성: 동일한 답변을 다양한 표현으로 해석 여부
* 과도한 프롬프트 의존성: 평가가 특정 프롬프트에 치우침. 단일 템플릿으로 모델 비교할 경우 편향된 결과 유도 가능(promptEval 지적)
* 비용, 리소스 제한: 다양한 프롬프트를 모두 평가하기 어려움. 수백 개 프롬프트를 일일이 평가하기엔 비용/시간 부담 큼
* 설계자 주관성: 평가 지표나 기준이 사람마다 다름
* 프롬프트 결함 영향: 입력 구조/형식 오류 등이 왜곡 유발
& 재현성 & 비교 가능성 낮음: 동일 평가 조건 재실험 어려움

#### 모델의 성능 평가에 어려움을 주는 요인
* 맥락 의존성과 주관성
  * task-dependent
    * 각 작업(b2c, b2b 등)마다 좋은 작업 결과의 기준이 다름
    * 요약에서는 간결성과 정보성을 우선하지만 프로그래밍에서는 코드의 적확성과 예외처리, 효율성이 우선됨
  * stakeholder-dependent(이해관계자)
    * 같은 출력도 어떤 관점에 따라 소비되느냐에 평가가 다를 수 있음
    * 최종 사용자, 실 수요자, 규제기관 등의 stakeholder에 따라 선호하는 경향이 달라짐
    * model의 provider에 따라 답변의 경향이 달라지는 경우도 포함
  * context-dependent
    * 사용하는 맥락에 따라 허요오디는 오차가 다름
    * 일상 사용에서는 동일한 오류에 있어서도 관대하지만, 전문가 사용이나 고위험 결정을 목적으로 하는 결우에는 더 엄밀하고 정확해야 함
  * 종합
    * 세가지의 축을 겹쳐서 모델의 답변의 패턴을 검증해야 함
    * llm의 답변에 걸친 세 가지 의존성을 잘 검증하면서 이를 기반으로 좋은 답변을 정의하는 것이 권장됨
* 측정 불가능한 중요 능력들
  * 쉽게 측정이 가능한 항목: 정량적이면서, 재현 가능하며 객관적이고 구체적인 지표
    * 정확도, 속도, 일관성, 답변 길이
  * 측정이 까다롭고 어려운 항목: 정성적 요소의 개입이 크며, 재현이 어렵고 사람마다 다른 평가 기준이 세워질 수 있는 경우
    * 창의성 공감, 윤리성, 상식에 기반한 답변
  * 종합
    * 모델을 평가함에 있어서, 측정 가능한 부분을 평가하고 전부인 것처럼 여기면 모델이 필요한 작업에 가지는 역량을 전부 평가하기 어려움
* 벤치마크 과발전과 포화