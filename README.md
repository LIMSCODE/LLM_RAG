# 프로젝트 개요
##### 1. finetuning_framework.ipynb 에서 GPT-2 모델을 chip2.csv 데이터로 파인튜닝
##### 2. 구글드라이브에 파인튜닝된 모델을 저장한다.
##### 3. Rag with Finetuned model.ipynb 에서 구글드라이브에 저장된 파인튜닝된 모델을 호출 
##### 4. 질문한것 + rag이용하여 구글검색한결과 => 모델입력으로 사용







		

# 프로젝트 구조
## finetuning_framework.ipynb 
##### chip2.csv데이터셋 가공, 사용자토큰적용함수(<QUERY>질문) 적용
##### chip2.csv로 GPT-2모델 파인튜닝 (trainer = Trainer(...))
##### 파인튜닝된모델을 구글드라이브에 저장 (trainer.save_model(model_save_path))

## Rag with Finetuned model.ipynb
##### 파인튜닝된모델 불러옴 (model = AutoModelForCausalLM.from_pretrained(model_load_path))
##### 모델파라미터세팅 (hf_pipeline = pipeline(...)
##### rag_query_with_search에서 질문 + 구글검색결과(google_search)를 모델입력으로사용 
##### hf_pipeline(input_text)로 모델답변생성 
