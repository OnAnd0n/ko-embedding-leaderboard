
# 한국어 오픈소스 임베딩 모델 리더보드
## ko-embedding-leaderboard

- MTEB를 custom하여 오픈소스 임베딩 모델을 평가 (데이터셋 일부 수정)
- 평가 코드 업로드 예정
- IR / Clustering 평가 Dataset 추가 예정
- HuggingFace에 기재된 대로 진행하되, SentenceTransformer > Transformers 의 우선순위로 모델 load.
  (단, Flagembedding으로만 기재된 경우, SentenceTransformer와 Transformers 중 높은 성능의 것으로 기입  //  Flagembedding로 Load 필요시, 추후 진행)
- pair sentence로 존재하는 Dataset 중, 중복 pair는 제거 ( (A, B) = (B, A) )
- LLM Based 임베딩 모델은 fp16/bf16으로 평가
- HuggingFace에 Query_fix가 기재된 경우, 추가 (IR에 대해서만 Query_fix가 명시되어 있을 경우에는 MTEB Instruction 기준으로 적용해보고, 만일 더 성능이 높다면 그대로 인정)
- 문의 사항이나, 평가가 필요한 모델은 issue에 남겨주세요.
- 잘못된 부분에 대한 조언/멘트는 감사히 받겠습니다.

평가 방식 살펴보기 : [MTEB 코드 살펴보기 (2)](https://introduce-ai.tistory.com/entry/%EC%9E%84%EB%B2%A0%EB%94%A9-%EB%AA%A8%EB%8D%B8-%ED%8F%89%EA%B0%80-MTEB-%EC%BD%94%EB%93%9C-%EC%82%B4%ED%8E%B4%EB%B3%B4%EA%B8%B0-2-Custom-Model-%ED%8F%89%EA%B0%80) 


### 평가 Metric
- STS : mean of {pearson, spearman, cosine_pearson, cosine_spearman, ..., euclidean_spearman}
- NLI : average precision
- Clustering : v-measure
- Retrieval : mean of NDCG @ 5, 10
- Weighted_Average => Retrieval : 33.3%,  Clustering : 33.3%, [NLI, STS] : 33.3%

# 종합 순위
|                                                                  |   STS_Average |   NLI_Average |   Clustering_Average |   Retrieval_Average |   Weighted_Average |   Rank |
|:-----------------------------------------------------------------|--------------:|--------------:|---------------------:|--------------------:|-------------------:|-------:|
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |         85.55 |         79.48 |                67.34 |               74.15 |              65.5  |      1 |
| intfloat/multilingual-e5-large-instruct                          |         82.24 |         65.69 |                70.4  |               71.74 |              63.82 |      2 |
| dragonkue/snowflake-arctic-embed-l-v2.0-ko                       |         81.9  |         60.21 |                63.82 |               78.13 |              63.11 |      3 |
| nlpai-lab/KURE-v1                                                |         83.37 |         64.79 |                61.6  |               75.67 |              62.22 |      4 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |         83.26 |         66.86 |                59.68 |               75.32 |              61.68 |      5 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |         79.97 |         67.21 |                65.2  |               69.63 |              61.3  |      6 |
| nlpai-lab/KoE5                                                   |         81.36 |         60.27 |                60.39 |               75.18 |              60.93 |      7 |
| BAAI/bge-multilingual-gemma2-fp16                                |         83.78 |         76.44 |                58.76 |               70.46 |              60.88 |      8 |
| BAAI/bge-m3                                                      |         83.46 |         65.32 |                58.27 |               73.55 |              60.47 |      9 |
| Snowflake/snowflake-arctic-embed-l-v2.0                          |         76.89 |         58.95 |                58.94 |               75.56 |              59.93 |     10 |
| dragonkue/BGE-m3-ko                                              |         84.1  |         62.01 |                55.47 |               75.44 |              59.87 |     11 |
| FronyAI/frony-embed-medium-ko-v1                                 |         79.44 |         60.53 |                58.26 |               72.57 |              59.16 |     12 |
| facebook/drama-1b-fp16                                           |         80.76 |         61.09 |                51.1  |               70.92 |              56.43 |     13 |
| upskyy/bge-m3-korean                                             |         84.67 |         70.82 |                42.74 |               67.91 |              54.16 |     14 |

#
#
#

# STS
|                                                                  |   KLUE-STS |   Kor-STS |   STS17 |   STS_Average |   Rank |
|:-----------------------------------------------------------------|-----------:|----------:|--------:|--------------:|-------:|
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |      89.65 |     83.3  |   83.69 |         85.55 |      1 |
| upskyy/bge-m3-korean                                             |      86.73 |     82.82 |   84.45 |         84.67 |      2 |
| dragonkue/BGE-m3-ko                                              |      87.35 |     81.76 |   83.19 |         84.1  |      3 |
| BAAI/bge-multilingual-gemma2-fp16                                |      88.94 |     81.29 |   81.1  |         83.78 |      4 |
| BAAI/bge-m3                                                      |      86.8  |     80.98 |   82.59 |         83.46 |      5 |
| nlpai-lab/KURE-v1                                                |      87.48 |     80.97 |   81.67 |         83.37 |      6 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |      85.94 |     81.22 |   82.63 |         83.26 |      7 |
| intfloat/multilingual-e5-large-instruct                          |      85.65 |     79.43 |   81.65 |         82.24 |      8 |
| dragonkue/snowflake-arctic-embed-l-v2.0-ko                       |      86.33 |     78.74 |   80.64 |         81.9  |      9 |
| nlpai-lab/KoE5                                                   |      85.1  |     79.01 |   79.96 |         81.36 |     10 |
| facebook/drama-1b-fp16                                           |      84.65 |     78    |   79.63 |         80.76 |     11 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |      80.81 |     78.79 |   80.3  |         79.97 |     12 |
| FronyAI/frony-embed-medium-ko-v1                                 |      78.9  |     78.2  |   81.22 |         79.44 |     13 |
| Snowflake/snowflake-arctic-embed-l-v2.0                          |      82.51 |     73.61 |   74.55 |         76.89 |     14 |


# NLI
|                                                                  |   KLUE-NLI |   Kor-NLI |   PawsX-PairClassification |   NLI_Average |   Rank |
|:-----------------------------------------------------------------|-----------:|----------:|---------------------------:|--------------:|-------:|
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |      80.19 |     89.18 |                      69.07 |         79.48 |      1 |
| BAAI/bge-multilingual-gemma2-fp16                                |      81.09 |     89.56 |                      58.66 |         76.44 |      2 |
| upskyy/bge-m3-korean                                             |      75.72 |     84.5  |                      52.23 |         70.82 |      3 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |      68.29 |     80.78 |                      52.56 |         67.21 |      4 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |      69.16 |     78.84 |                      52.58 |         66.86 |      5 |
| intfloat/multilingual-e5-large-instruct                          |      69.87 |     75.51 |                      51.69 |         65.69 |      6 |
| BAAI/bge-m3                                                      |      68.34 |     74.88 |                      52.75 |         65.32 |      7 |
| nlpai-lab/KURE-v1                                                |      67.34 |     75.12 |                      51.92 |         64.79 |      8 |
| dragonkue/BGE-m3-ko                                              |      65.41 |     68.71 |                      51.92 |         62.01 |      9 |
| facebook/drama-1b-fp16                                           |      64.6  |     68.14 |                      50.52 |         61.09 |     10 |
| FronyAI/frony-embed-medium-ko-v1                                 |      62.43 |     67.33 |                      51.83 |         60.53 |     11 |
| nlpai-lab/KoE5                                                   |      61.81 |     66.22 |                      52.79 |         60.27 |     12 |
| dragonkue/snowflake-arctic-embed-l-v2.0-ko                       |      63.27 |     65.04 |                      52.32 |         60.21 |     13 |
| Snowflake/snowflake-arctic-embed-l-v2.0                          |      59.86 |     63.78 |                      53.2  |         58.95 |     14 |

# Clustering
|                                                                  |   sib2000 |   clustering_klue_mrc_context_domain |   clustering_klue_mrc_ynat_title |   Clustering_Average |   Rank |
|:-----------------------------------------------------------------|----------:|-------------------------------------:|---------------------------------:|---------------------:|-------:|
| intfloat/multilingual-e5-large-instruct                          |     56.67 |                                81.85 |                            72.67 |                70.4  |      1 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |     40.31 |                                80.1  |                            81.6  |                67.34 |      2 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |     45.56 |                                81.8  |                            68.24 |                65.2  |      3 |
| dragonkue/snowflake-arctic-embed-l-v2.0-ko                       |     34.46 |                                75.62 |                            81.38 |                63.82 |      4 |
| nlpai-lab/KURE-v1                                                |     39.21 |                                75.08 |                            70.52 |                61.6  |      5 |
| nlpai-lab/KoE5                                                   |     36.22 |                                73.29 |                            71.67 |                60.39 |      6 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |     33.53 |                                80.24 |                            65.26 |                59.68 |      7 |
| Snowflake/snowflake-arctic-embed-l-v2.0                          |     47.8  |                                71.71 |                            57.31 |                58.94 |      8 |
| BAAI/bge-multilingual-gemma2-fp16                                |     50.92 |                                75.39 |                            49.96 |                58.76 |      9 |
| BAAI/bge-m3                                                      |     33.01 |                                71.85 |                            69.96 |                58.27 |     10 |
| FronyAI/frony-embed-medium-ko-v1                                 |     41.02 |                                72.11 |                            61.66 |                58.26 |     11 |
| dragonkue/BGE-m3-ko                                              |     29.49 |                                70.81 |                            66.1  |                55.47 |     12 |
| facebook/drama-1b-fp16                                           |     36.06 |                                71.07 |                            46.18 |                51.1  |     13 |
| upskyy/bge-m3-korean                                             |     22.08 |                                73.49 |                            32.66 |                42.74 |     14 |

# Retrieval
|                                                                  |   Ko-StrategyQA |   AutoRAGRetrieval |   PublicHealthQA |   XPQARetrieval |   facebook/belebele |   Retrieval_Average |   Rank |
|:-----------------------------------------------------------------|----------------:|-------------------:|-----------------:|----------------:|--------------------:|--------------------:|-------:|
| dragonkue/snowflake-arctic-embed-l-v2.0-ko                       |           80.01 |              90.33 |            82.56 |           42.69 |               95.07 |               78.13 |      1 |
| nlpai-lab/KURE-v1                                                |           79.2  |              86.66 |            81.1  |           36.49 |               94.91 |               75.67 |      2 |
| Snowflake/snowflake-arctic-embed-l-v2.0                          |           79.57 |              83.61 |            80.78 |           41.33 |               92.51 |               75.56 |      3 |
| dragonkue/BGE-m3-ko                                              |           78.75 |              86.65 |            80.49 |           36.42 |               94.88 |               75.44 |      4 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |           79.98 |              79.71 |            87.45 |           37.35 |               92.09 |               75.32 |      5 |
| nlpai-lab/KoE5                                                   |           78.85 |              84.46 |            83.68 |           34.73 |               94.2  |               75.18 |      6 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |           80.29 |              75.12 |            80.93 |           39.86 |               94.56 |               74.15 |      7 |
| BAAI/bge-m3                                                      |           78.58 |              82.32 |            79.36 |           34.64 |               92.87 |               73.55 |      8 |
| FronyAI/frony-embed-medium-ko-v1                                 |           76.36 |              78.41 |            81.57 |           34.04 |               92.49 |               72.57 |      9 |
| intfloat/multilingual-e5-large-instruct                          |           79.59 |              74.56 |            81.35 |           31.46 |               91.76 |               71.74 |     10 |
| facebook/drama-1b-fp16                                           |          nan    |             nan    |            80.06 |           36.97 |               95.73 |               70.92 |     11 |
| BAAI/bge-multilingual-gemma2-fp16                                |           78.2  |              75.64 |            65.6  |           37.08 |               95.79 |               70.46 |     12 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |           70.17 |              75.34 |            79.11 |           36.72 |               86.8  |               69.63 |     13 |
| upskyy/bge-m3-korean                                             |           74.2  |              71.66 |            76.53 |           30.27 |               86.91 |               67.91 |     14 |

# Task별 Query_fix / Instruction
|                                                                  | STS                                                                               | NLI                                                                                            | Clustering                                                                                     | IR                         |
|:-----------------------------------------------------------------|:----------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------|:---------------------------|
| BAAI/bge-m3                                                      |                                                                                   |                                                                                                |                                                                                                |                            |
| dragonkue/BGE-m3-ko                                              |                                                                                   |                                                                                                |                                                                                                |                            |
| upskyy/bge-m3-korean                                             |                                                                                   |                                                                                                |                                                                                                |                            |
| nlpai-lab/KoE5                                                   |                                                                                   |                                                                                                |                                                                                                |                            |
| nlpai-lab/KURE-v1                                                |                                                                                   |                                                                                                |                                                                                                |                            |
| FronyAI/frony-embed-medium-ko-v1                                 |                                                                                   |                                                                                                |                                                                                                | github issue 요청사항 적용 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |                                                                                   |                                                                                                |                                                                                                |                            |
| Snowflake/snowflake-arctic-embed-l-v2.0                          | query:                                                                            | query:                                                                                         | query:                                                                                         | 허깅페이스 기준 적용       |
| dragonkue/snowflake-arctic-embed-l-v2.0-ko                       | query:                                                                            | query:                                                                                         | query:                                                                                         | 허깅페이스 기준 적용       |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        | (큰 차이는 없었음)None or Instruct: retrieve semantically similar text.<br>Query: |                                                                                                | Instruct: Identify the topic or theme of the given texts<br>Query:                             | 허깅페이스 기준 적용       |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           | Instruct: retrieve semantically similar text.<br>Query:                           | Instruct: retrieve semantically similar text.<br>Query:                                        | Instruct: Given a web search query, retrieve relevant passages that answer the query<br>Query: | 허깅페이스 기준 적용       |
| BAAI/bge-multilingual-gemma2-fp16                                | <instruct>retrieve semantically similar text.<br><query>                          | <instruct>retrieve semantically similar text.<br><query>                                       | <instruct>Identify the topic or theme of the given texts<br><query>                            | 허깅페이스 기준 적용       |
| intfloat/multilingual-e5-large-instruct                          | Instruct: retrieve semantically similar text.<br>Query:                           | Instruct: Determine whether the two given sentences express the same meaning or not.<br>Query: | Instruct: Identify the topic or theme of the given texts<br>Query:                             | 허깅페이스 기준 적용       |
| facebook/drama-1b-fp16                                           | Query:                                                                            | Query:                                                                                         | Query:                                                                                         | 허깅페이스 기준 적용       |


https://onand0n.github.io/ko-embedding-leaderboard/



