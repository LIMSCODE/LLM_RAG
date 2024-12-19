# 프로젝트 개요

##### 1. `finetuning_framework.ipynb` 에서 GPT-2 모델을 `chip2.csv` 데이터로 파인튜닝
##### 2. 구글드라이브에 파인튜닝된 모델을 저장한다.
##### 3. `Rag with Finetuned model.ipynb` 에서 구글드라이브에 저장된 파인튜닝된 모델을 호출
##### 4. 질문한 것 + RAG 이용하여 구글 검색한 결과 => 모델 입력으로 사용



# 프로젝트 구조

## `finetuning_framework.ipynb`

##### - `chip2.csv` 데이터셋 가공, 사용자 토큰 적용 함수 (`<QUERY>` 질문) 적용
##### - `chip2.csv`로 GPT-2 모델 파인튜닝 (`trainer = Trainer(...)`)
##### - 파인튜닝된 모델을 구글드라이브에 저장 (`trainer.save_model(model_save_path)`)

## `Rag with Finetuned model.ipynb`

##### - 파인튜닝된 모델 불러옴 (`model = AutoModelForCausalLM.from_pretrained(model_load_path)`)
##### - 모델 파라미터 세팅 (`hf_pipeline = pipeline(...)`)
##### - `rag_query_with_search`에서 질문 + 구글 검색 결과(`google_search`)를 모델 입력으로 사용
##### - `hf_pipeline(input_text)`로 모델 답변 생성
