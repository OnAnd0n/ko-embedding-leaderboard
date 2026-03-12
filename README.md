# 한국어 오픈소스 임베딩 모델 리더보드 (Version 2.)
## ko-embedding-leaderboard

- MTEB를 custom하여 오픈소스 임베딩 모델을 평가 (데이터셋 일부 수정)
- IR 평가 Dataset 추가 예정
- HuggingFace에 기재된 대로 진행하되, SentenceTransformer > Transformers 의 우선순위로 모델 load.
- HuggingFace에 Query_fix가 기재된 경우, 적용
- 문의 사항이나, 평가가 필요한 모델은 issue에 남겨주세요.
- 잘못된 부분에 대한 조언/멘트는 감사히 받겠습니다.
- 평가 방식 살펴보기 : [MTEB 코드 살펴보기 (2)](https://introduce-ai.tistory.com/entry/%EC%9E%84%EB%B2%A0%EB%94%A9-%EB%AA%A8%EB%8D%B8-%ED%8F%89%EA%B0%80-MTEB-%EC%BD%94%EB%93%9C-%EC%82%B4%ED%8E%B4%EB%B3%B4%EA%B8%B0-2-Custom-Model-%ED%8F%89%EA%B0%80) 

※ Version 2부터는 Clusetering, NLI 등은 평가 하지 않고 IR만 평가합니다. [Version 1 확인하기](https://github.com/OnAnd0n/ko-embedding-leaderboard/blob/main/v1/v1.md) 


### 평가 Metric
- Retrieval : mean of NDCG @ 5, 10



# Sparse 임베딩 모델 IR 순위
|                                       |   Ko-StrategyQA |   AutoRAGRetrieval |   PublicHealthQA |   facebook/belebele |   webfaq-retrieval |   miracl/miracl |   Sparse_Retrieval_Average |   Rank |
|:--------------------------------------|----------------:|-------------------:|-----------------:|--------------------:|-------------------:|----------------:|---------------------------:|-------:|
| yjoonjang/splade-ko-v1                |           72.9  |              94.23 |            78.68 |               95.65 |              78.93 |           51.29 |                      78.61 |      1 |
| telepix/PIXIE-Splade-Preview          |           71.59 |              95.97 |            79.1  |               95.44 |              78.1  |           49.22 |                      78.24 |      2 |
| yjoonjang/inference-free-splade-ko-v1 |           70.53 |              93.83 |            72.46 |               93.55 |              78.63 |           50.42 |                      76.57 |      3 |


# Dense 임베딩 모델 IR 순위
|                                            |   Ko-StrategyQA |   AutoRAGRetrieval |   PublicHealthQA |   law_ir-ko |   webfaq-retrieval |   squad-kor-v1 |   Retrieval_Average |   Rank |
|:-------------------------------------------|----------------:|-------------------:|-----------------:|------------:|-------------------:|---------------:|--------------------:|-------:|
| dragonkue/snowflake-arctic-embed-l-v2.0-ko |           80.01 |              90.33 |            82.56 |       76.38 |              85.97 |          93.35 |               84.77 |      1 |
| telepix/PIXIE-Rune-v1.0                    |           79.54 |              89.39 |            83.18 |       76.01 |              85.49 |          94.44 |               84.68 |      2 |
| Qwen/Qwen3-Embedding-4B-bf16               |           82.07 |              82.8  |            85.57 |       76.48 |              83.98 |          90.06 |               83.49 |      3 |
| nlpai-lab/KURE-v1                          |           79.2  |              86.66 |            81.1  |       73.21 |              85.06 |          93.35 |               83.1  |      4 |
| Snowflake/snowflake-arctic-embed-l-v2.0    |           79.57 |              83.61 |            80.78 |       74.88 |              85.44 |          90.96 |               82.54 |      5 |
| BAAI/bge-m3                                |           78.58 |              82.32 |            79.36 |       70.72 |              84.15 |          90.07 |               80.87 |      6 |
| intfloat/multilingual-e5-large-instruct    |           79.59 |              74.56 |            81.35 |       73.34 |              81.69 |          89.34 |               79.98 |      7 |
| Qwen/Qwen3-Embedding-0.6B-bf16             |           75.76 |              82.06 |            78.14 |       71.1  |              80.35 |          84.53 |               78.66 |      8 |