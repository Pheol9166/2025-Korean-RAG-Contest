# 2025 국립국어원 AI 말평 한국어 어문 규범 기반 생성(RAG) 가 유형

## Final Rank
32등(전체 60팀)
  
|Final Score|Exact Match|BLEURT|BERTScore|ROUGE-1|
|---|---|---|---|---|
|51.85|50.80|51.84|74.52|32.32|

## Attempts
- Qwen3-8b 8bit quantization + QLoRA
  - 8bit 양자화한 후 train data를 기반으로 QLoRA 학습 진행
  - test data 평가  
  <br>
  
  |Final Score|Exact Match|BLEURT|BERTScore|ROUGE-1|
  |---|---|---|---|---|
  |47.80|43.17|51.02|74.07|32.23|

- Qwen3-32b 4bit quantization + QLoRA
  - 가능한 하드웨어 제약 내에서 가장 파라미터수가 큰 모델 선정
  - test data 평가, 가장 높은 점수
  <br>
  
  |Final Score|Exact Match|BLEURT|BERTScore|ROUGE-1|
  |---|---|---|---|---|
  |51.85|50.80|51.84|74.52|32.32|

- Qwen3-32b 4bit quantization + QLoRA + RAG(KURE-v1)
  - langchain 구조 사용 및 few-shot prompting
  - 임베딩 모델로는 한국어 검색에 특화된 KURE-v1 사용
  - dev data 평가
  <br>

  |Final Score|Exact Match|BLEURT|BERTScore|ROUGE-1|
  |---|---|---|---|---|
  |53.54|54.33|51.64|74.48|32.16|

- Qwen3-32b 4bit quantization + QLoRA + RAG(KoELECTRA v3)
  - 하드웨어 제약으로 인해 임베딩 모델 변경 및 프롬프트 수정
  - dev data 평가
  <br>

  |Final Score|Exact Match|BLEURT|BERTScore|ROUGE-1|
  |---|---|---|---|---|
  |50.40|48.03|51.19|74.37|32.77|

- Qwen3-32b 4bit quantization + QLoRA + RAG(KURE-v1)
  - 임베딩 모델 재변경
  - 프롬프트 형태를 chat prompt template으로 변경, tokenizer의 `apply_chat_template` 메소드로 적용
  - dev data 평가
  <br>

  |Final Score|Exact Match|BLEURT|BERTScore|ROUGE-1|
  |---|---|---|---|---|
  |51.72|50.39|53.08|74.37|31.72|

- Qwen3-14b 8bit quantization + QLoRA + RAG(KURE-v1)
  - LLM 변경
  - dev data 평가
  <br>

  |Final Score|Exact Match|BLEURT|BERTScore|ROUGE-1|
  |---|---|---|---|---|
  |51.85|51.18|51.35|73.99|32.23|

- Qwen3-14b 8bit quantization + QLoRA + RAG(KURE-v1) + Query LLM(Qwen3-14b)
  - retriever 성능 향상을 위해 query 재작성을 도와줄 LLM 도입
  - 하드웨어를 아끼기 위해 generator에 사용되는 LLM을 그대로 사용
  - dev data 평가
  <br>

  |Final Score|Exact Match|BLEURT|BERTScore|ROUGE-1|
  |---|---|---|---|---|
  |53.61|54.33|51.41|74.57|32.71|

- Qwen3-14b 8bit quantization + QLoRA + RAG(KURE-v1) + Query LLM(EXAONE-4.0-1.2b)
  - Query LLM 변경 및 프롬프트 수정
  - dev data 평가
  <br>

  |Final Score|Exact Match|BLEURT|BERTScore|ROUGE-1|
  |---|---|---|---|---|
  |55.81|57.48|52.86|75.53|34.02|

- Qwen3-14b 8bit quantization + QLoRA + RAG(KURE-v1) + Query LLM(EXAONE-4.0-1.2b)
  - test data 평가
  <br>

  |Final Score|Exact Match|BLEURT|BERTScore|ROUGE-1|
  |---|---|---|---|---|
  |50.24|48.99|50.20|74.11|30.16|

- EXAONE-4.0-32b 4bit quantization + RAG(KURE-v1) + Query LLM(EXAONE-4.0-32b)
   - LLM 변경
   - dev data 평가
  <br>

  |Final Score|Exact Match|BLEURT|BERTScore|ROUGE-1|
  |---|---|---|---|---|
  |48.60|47.24|48.36|73.42|28.11|


## Feedback
평가 체계가 exact match와 descriptive_average(BLEURT, BERTScore, ROUGE-1)의 평균이라 exact match 향상을 주된 목표로 하였음. 때문에 주로 retriever의 성능 향상에 치중했었는데, exact match가 오르기 위해선 문법 교정 능력을 올렸어야 함. 즉, retriever도 retriever지만 LLM의 추론 능력 향상과 그를 위한 hyperparameter 조정(혹은 학습 파라미터 조정)이 더 중요했다고 생각함.  
또한 dev data의 평가 결과의 향상이 test data의 향상으로 이어지는 것은 아니었기에 test data 평가를 더 많이 해보고 방법을 고안했어야 한다고 생각함. 여러 방법을 거쳤지만 정작 test data의 평가는 기본 모델을 썼을 때보다 좋지 않은 것으로 봐서 아주 많은 방법들을 적용하는 것은 성능에 그다지 좋은 영향을 주지는 못하는 것 같음.
