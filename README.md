### LLM + RAG 결합 질문답변시스템
#### 프로젝트 개요
1. `finetuning_framework.ipynb` 에서 GPT-2 모델을 `chip2.csv` 데이터로 파인튜닝 <br>
2. 구글드라이브에 파인튜닝된 모델을 저장한다. <br>
3. `Rag with Finetuned model.ipynb` 에서 구글드라이브에 저장된 파인튜닝된 모델을 호출 <br>
4. 질문입력 + 구글API검색결과 => 모델입력으로 통합하여 모델이 답변생성 (RAG)  <br>

#### 프로젝트 구조
#### `finetuning_framework.ipynb`
`chip2.csv` 데이터셋 가공, 사용자 토큰 적용 함수 (`<QUERY>` 질문) 적용 <br>
`chip2.csv`로 GPT-2 모델 파인튜닝 (`trainer = Trainer(...)`) <br>
파인튜닝된 모델을 구글드라이브에 저장 (`trainer.save_model(model_save_path)`) <br>
#### `Rag with Finetuned model.ipynb`
파인튜닝된 모델 불러옴 (`model = AutoModelForCausalLM.from_pretrained(model_load_path)`) <br>
모델 파라미터 세팅 (`hf_pipeline = pipeline(...)`) <br>
`rag_query_with_search`에서 질문 + 구글 검색 결과(`google_search`)를 모델 입력으로 사용 <br>
`hf_pipeline(input_text)`로 모델 답변 생성 <br> 
### `강화학습적용`
1) 보상모델(RL) 정의 및 학습
{질문,사람점수매긴답변}쌍에서 높은점수의 답변에 높은보상값을 줘서 선호되도록 모델훈련
2) 강화학습(TRL) 적용
ppo_trainer.generate() :답변생성, 답변을 보상모델에 입력하여 보상값얻음
ppo_trainer.step() :보상값 기반 모델학습 (TRL이 보상값기반 기존답변과 차이 고려하여 모델변경)
