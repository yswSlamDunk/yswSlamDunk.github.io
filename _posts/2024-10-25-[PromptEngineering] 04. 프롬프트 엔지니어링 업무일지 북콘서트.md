---
layout : single
title : "[PromptEngineering] 04. 프롬프트 엔지니어링 업무일지 북미팅"
categories : [PromptEngineering, LLM]
tag : [프롬프트 테스트 규칙, 언어 모델의 한계, 강수진]
---

#### 프롬프트는 언어인가?
* Thingking Fast and Slow 책
   * 인간은 두 개의 사고를 함(빠른 사고와 느린 사고)
   * LLM은 빠른 사고를 잘 하지만 느린 사고를 잘 못함
   * 프롬프트 엔지니어링은 느린 사고를 잘 할 수 있도록 해줘야 함
   
* chatGPT-o1 관련 내용
   * 테디노트님의 고객 피드백을 들어보면, 느린 생각을 빠르게 진행하는게 중요함
   * 느린 사고의 품질을 높이는 것은 문제가 어려움이 없음
   * 느린(속도 뿐 아니라 입체적인) 사고
   * LLM은 문화적인 특수성으로 인해 성과가 좋지 못함
   
#### 프롬프트 엔지니어링으로 언어의 맥락과 뉘앙스를 어떻게 반영할 수 있나?
* The Silent Language
   * LLM은 비언어적인 내용에서 문제가 있음
   * 고맥락 언어: 한국어
   * Semantics vs Pragmatics
      * Semantics: Conventional, Constant, Truth-conditional
      * Pragmatics: Conversational, Context Dependent, Non-Truth-Conditioanl
         * Pragmatics를 LLM이 잘 이해하도록 하기 위해서 노력함

#### 프롬프트를 어떻게 제작하나?
* Prompt Anatomy
   * Instruction
   * Context
   * Input Data
   * Ouput Indicator
* 프롬프트에 입력한 정보가 반영이 되었는지를 모두 확인함
* 고퀄리티의 프롬프트를 작성해야 한다면, 문장을 형태소 단위까지 분해하여, Sementic Loss를 줄이려고 노력함
* 프롬프트 제너레이터를 사용하지말고 직접 타이핑 하는 것이 중요함
* Interactioin 사이에 "---"를 입력하는 것이 중요함

#### LLM 기반 개발 어떻게 하나? 그리고 어려운 점
* 파이프라인에 LLM을 여러번 사용하는데, 프롬프트 엔지니어링을 통해 추론을 가장 적게해서 중간과정을 생략 가능함
* iterative process for prompt development
* 평가는 LLM as a Judge를 기반으로 진행함
* 프롬프트의 한끗은 도메인 지식 

#### 메타 프롬프트에 대한 생각과 
* 메타 프롬프트: 만들어진 프롬프트를 LLM을 이용해서 optimize 하는 것
* 강수진 박사님은 메타 프롬프트는 한계가 있다고 생각함
* 메타 프롬프트를 시행하면 general한 단어가 나타남
* 프롬프트의 목적이 단순한 정보제공이면, 메타 프롬프트가 적합
* 특정 상황, 대상이라면 메타 프롬프트가 아닌 직접 프롬프트 작성이 더 좋음

#### 질문 
* word bank 기법을 사용하여 학습 외의 단어를 활용함

#### 사용자 문제
* 문제1: ai 엔지니어는 기술이 있지만 실제 사용자의 문제는 모른다.
* 문제2: 제품 사용자의 문제는 분명하지만 해결 할 방법을 모른다.

