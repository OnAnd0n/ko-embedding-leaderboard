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
|                                       |   Ko-StrategyQA |   AutoRAGRetrieval |   PublicHealthQA |   facebook/belebele |   WebFAQRetrieval |   miracl/miracl |   Sparse_Retrieval_Average |   Rank |
|:--------------------------------------|----------------:|-------------------:|-----------------:|--------------------:|-------------------:|----------------:|---------------------------:|-------:|
| yjoonjang/splade-ko-v1                |           72.9  |              94.23 |            78.68 |               95.65 |              78.93 |           51.29 |                      78.61 |      1 |
| telepix/PIXIE-Splade-Preview          |           71.59 |              95.97 |            79.1  |               95.44 |              78.1  |           49.22 |                      78.24 |      2 |
| yjoonjang/inference-free-splade-ko-v1 |           70.53 |              93.83 |            72.46 |               93.55 |              78.63 |           50.42 |                      76.57 |      3 |


# Dense 임베딩 모델 IR 순위
|                                            |                                            |   Ko-StrategyQA |   AutoRAGRetrieval |   PublicHealthQA |   LawIRKo |   WebFAQRetrieval |   SQuADKorV1Retrieval |   MIRACLRetrievalHardNegative |   Retrieval_Average |   Rank |
|:-------------------------------------------|----------------:|-------------------:|-----------------:|----------:|------------------:|----------------------:|------------------------------:|--------------------:|-------:|
| perplexity-ai/pplx-embed-v1-4b             |           82.25 |              82.27 |            89.54 |     76.44 |             89.51 |                 93.91 |                         65.6  |               82.79 |      1 |
| dragonkue/snowflake-arctic-embed-l-v2.0-ko |           79.69 |              90.64 |            82.56 |     76.38 |             85.98 |                 94.34 |                         65.38 |               82.14 |      2 |
| telepix/PIXIE-Rune-v1.0                    |           79.54 |              89.39 |            83.18 |     76.02 |             85.5  |                 94.43 |                         62.93 |               81.57 |      3 |
| Qwen/Qwen3-Embedding-4B                    |           81.89 |              83.04 |            86.54 |     76.79 |             84.16 |                 90.12 |                         67.06 |               81.37 |      4 |
| nlpai-lab/KURE-v1                          |           79.2  |              86.66 |            81.1  |     73.22 |             85.05 |                 93.35 |                         66.75 |               80.76 |      5 |
| jinaai/jina-embeddings-v5-text-small       |           80.06 |              82.52 |            86.24 |     74.01 |             84.2  |                 88.91 |                         66.12 |               80.29 |      6 |
| Snowflake/snowflake-arctic-embed-l-v2.0    |           79.57 |              83.60 |            80.78 |     74.89 |             85.45 |                 90.95 |                         64.75 |               80    |      7 |
| BAAI/bge-m3                                |           78.58 |              82.32 |            80.69 |     70.72 |             84.14 |                 90.07 |                         68.59 |               79.3  |      8 |
| google/embeddinggemma-300m                 |           79.25 |              81.02 |            81.54 |     67.5  |             84.4  |                 90.8  |                         62.81 |               78.19 |      9 |
| microsoft/harrier-oss-v1-0.6b              |           77.01 |              82.21 |            82.17 |     69.09 |             76.93 |                 91.95 |                         63.04 |               77.49 |     10 |
| intfloat/multilingual-e5-large-instruct    |           78.93 |              74.72 |            80.69 |     73.38 |             81.32 |                 89.08 |                         62.74 |               77.27 |     11 |
| Qwen/Qwen3-Embedding-0.6B                  |           75.55 |              81.51 |            78.51 |     71.48 |             80.54 |                 84.53 |                         59.03 |               75.88 |     12 |