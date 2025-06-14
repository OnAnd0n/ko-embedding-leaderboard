
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
| Qwen/Qwen3-Embedding-8B-bf16                                     |         89.36 |         77.71 |                65.79 |               78.73 |              66.74 |      1 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |         85.55 |         79.48 |                67.34 |               75.73 |              66.03 |      2 |
| intfloat/multilingual-e5-large-instruct                          |         82.24 |         65.69 |                70.4  |               73.4  |              64.37 |      3 |
| Qwen/Qwen3-Embedding-4B-bf16                                     |         89.2  |         76.4  |                58.74 |               77.68 |              63.87 |      4 |
| dragonkue/snowflake-arctic-embed-l-v2.0-ko                       |         81.9  |         60.21 |                63.82 |               79.44 |              63.54 |      5 |
| nlpai-lab/KURE-v1                                                |         83.37 |         64.79 |                61.6  |               77.24 |              62.74 |      6 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |         83.26 |         66.86 |                59.68 |               76.51 |              62.08 |      7 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |         79.97 |         67.21 |                65.2  |               71.88 |              62.05 |      8 |
| BAAI/bge-multilingual-gemma2-fp16                                |         83.78 |         76.44 |                58.76 |               72.41 |              61.53 |      9 |
| nlpai-lab/KoE5                                                   |         81.36 |         60.27 |                60.39 |               76.68 |              61.43 |     10 |
| Qwen/Qwen3-Embedding-0.6B-bf16                                   |         84.68 |         69.58 |                58.59 |               73.3  |              61.1  |     11 |
| BAAI/bge-m3                                                      |         83.46 |         65.32 |                58.27 |               75.32 |              61.06 |     12 |
| Snowflake/snowflake-arctic-embed-l-v2.0                          |         76.89 |         58.95 |                58.94 |               77.21 |              60.48 |     13 |
| dragonkue/BGE-m3-ko                                              |         84.1  |         62.01 |                55.47 |               77.04 |              60.4  |     14 |
| FronyAI/frony-embed-medium-arctic-ko-v2.5                        |         83.26 |         60.47 |                53.45 |               77.86 |              59.74 |     15 |
| facebook/drama-1b-fp16                                           |         80.76 |         61.09 |                51.1  |               77.29 |              58.56 |     16 |
| FronyAI/frony-embed-medium-ko-v2                                 |         80.23 |         61.14 |                53.75 |               74.02 |              58.3  |     17 |
| upskyy/bge-m3-korean                                             |         84.67 |         70.82 |                42.74 |               69.98 |              54.85 |     18 |

#
#
#

# STS
|                                                                  |   KLUE-STS |   Kor-STS |   STS17 |   STS_Average |   Rank |
|:-----------------------------------------------------------------|-----------:|----------:|--------:|--------------:|-------:|
| Qwen/Qwen3-Embedding-8B-bf16                                     |      88.74 |     89.68 |   89.65 |         89.36 |      1 |
| Qwen/Qwen3-Embedding-4B-bf16                                     |      88.63 |     89.21 |   89.77 |         89.2  |      2 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |      89.65 |     83.3  |   83.69 |         85.55 |      3 |
| Qwen/Qwen3-Embedding-0.6B-bf16                                   |      84.11 |     85.56 |   84.36 |         84.68 |      4 |
| upskyy/bge-m3-korean                                             |      86.73 |     82.82 |   84.45 |         84.67 |      5 |
| dragonkue/BGE-m3-ko                                              |      87.35 |     81.76 |   83.19 |         84.1  |      6 |
| BAAI/bge-multilingual-gemma2-fp16                                |      88.94 |     81.29 |   81.1  |         83.78 |      7 |
| BAAI/bge-m3                                                      |      86.8  |     80.98 |   82.59 |         83.46 |      8 |
| nlpai-lab/KURE-v1                                                |      87.48 |     80.97 |   81.67 |         83.37 |      9 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |      85.94 |     81.22 |   82.63 |         83.26 |     10 |
| FronyAI/frony-embed-medium-arctic-ko-v2.5                        |      83.86 |     82.01 |   83.92 |         83.26 |     10 |
| intfloat/multilingual-e5-large-instruct                          |      85.65 |     79.43 |   81.65 |         82.24 |     12 |
| dragonkue/snowflake-arctic-embed-l-v2.0-ko                       |      86.33 |     78.74 |   80.64 |         81.9  |     13 |
| nlpai-lab/KoE5                                                   |      85.1  |     79.01 |   79.96 |         81.36 |     14 |
| facebook/drama-1b-fp16                                           |      84.65 |     78    |   79.63 |         80.76 |     15 |
| FronyAI/frony-embed-medium-ko-v2                                 |      78.01 |     80.47 |   82.21 |         80.23 |     16 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |      80.81 |     78.79 |   80.3  |         79.97 |     17 |
| Snowflake/snowflake-arctic-embed-l-v2.0                          |      82.51 |     73.61 |   74.55 |         76.89 |     18 |


# NLI
|                                                                  |   KLUE-NLI |   Kor-NLI |   PawsX-PairClassification |   NLI_Average |   Rank |
|:-----------------------------------------------------------------|-----------:|----------:|---------------------------:|--------------:|-------:|
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |      80.19 |     89.18 |                      69.07 |         79.48 |      1 |
| Qwen/Qwen3-Embedding-8B-bf16                                     |      79.45 |     88.86 |                      64.83 |         77.71 |      2 |
| BAAI/bge-multilingual-gemma2-fp16                                |      81.09 |     89.56 |                      58.66 |         76.44 |      3 |
| Qwen/Qwen3-Embedding-4B-bf16                                     |      79.78 |     88.83 |                      60.59 |         76.4  |      4 |
| upskyy/bge-m3-korean                                             |      75.72 |     84.5  |                      52.23 |         70.82 |      5 |
| Qwen/Qwen3-Embedding-0.6B-bf16                                   |      71.81 |     82.14 |                      54.79 |         69.58 |      6 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |      68.29 |     80.78 |                      52.56 |         67.21 |      7 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |      69.16 |     78.84 |                      52.58 |         66.86 |      8 |
| intfloat/multilingual-e5-large-instruct                          |      69.87 |     75.51 |                      51.69 |         65.69 |      9 |
| BAAI/bge-m3                                                      |      68.34 |     74.88 |                      52.75 |         65.32 |     10 |
| nlpai-lab/KURE-v1                                                |      67.34 |     75.12 |                      51.92 |         64.79 |     11 |
| dragonkue/BGE-m3-ko                                              |      65.41 |     68.71 |                      51.92 |         62.01 |     12 |
| FronyAI/frony-embed-medium-ko-v2                                 |      63.08 |     68.57 |                      51.78 |         61.14 |     13 |
| facebook/drama-1b-fp16                                           |      64.6  |     68.14 |                      50.52 |         61.09 |     14 |
| FronyAI/frony-embed-medium-arctic-ko-v2.5                        |      61.39 |     68.1  |                      51.93 |         60.47 |     15 |
| nlpai-lab/KoE5                                                   |      61.81 |     66.22 |                      52.79 |         60.27 |     16 |
| dragonkue/snowflake-arctic-embed-l-v2.0-ko                       |      63.27 |     65.04 |                      52.32 |         60.21 |     17 |
| Snowflake/snowflake-arctic-embed-l-v2.0                          |      59.86 |     63.78 |                      53.2  |         58.95 |     18 |

# Clustering
|                                                                  |   sib2000 |   clustering_klue_mrc_context_domain |   clustering_klue_mrc_ynat_title |   Clustering_Average |   Rank |
|:-----------------------------------------------------------------|----------:|-------------------------------------:|---------------------------------:|---------------------:|-------:|
| intfloat/multilingual-e5-large-instruct                          |     56.67 |                                81.85 |                            72.67 |                70.4  |      1 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |     40.31 |                                80.1  |                            81.6  |                67.34 |      2 |
| Qwen/Qwen3-Embedding-8B-bf16                                     |     48.26 |                                68.97 |                            80.15 |                65.79 |      3 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |     45.56 |                                81.8  |                            68.24 |                65.2  |      4 |
| dragonkue/snowflake-arctic-embed-l-v2.0-ko                       |     34.46 |                                75.62 |                            81.38 |                63.82 |      5 |
| nlpai-lab/KURE-v1                                                |     39.21 |                                75.08 |                            70.52 |                61.6  |      6 |
| nlpai-lab/KoE5                                                   |     36.22 |                                73.29 |                            71.67 |                60.39 |      7 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |     33.53 |                                80.24 |                            65.26 |                59.68 |      8 |
| Snowflake/snowflake-arctic-embed-l-v2.0                          |     47.8  |                                71.71 |                            57.31 |                58.94 |      9 |
| BAAI/bge-multilingual-gemma2-fp16                                |     50.92 |                                75.39 |                            49.96 |                58.76 |     10 |
| Qwen/Qwen3-Embedding-4B-bf16                                     |     43.43 |                                63.31 |                            69.49 |                58.74 |     11 |
| Qwen/Qwen3-Embedding-0.6B-bf16                                   |     37.8  |                                73.41 |                            64.55 |                58.59 |     12 |
| BAAI/bge-m3                                                      |     33.01 |                                71.85 |                            69.96 |                58.27 |     13 |
| dragonkue/BGE-m3-ko                                              |     29.49 |                                70.81 |                            66.1  |                55.47 |     14 |
| FronyAI/frony-embed-medium-ko-v2                                 |     37.17 |                                66.49 |                            57.58 |                53.75 |     15 |
| FronyAI/frony-embed-medium-arctic-ko-v2.5                        |     31.31 |                                71.04 |                            58.01 |                53.45 |     16 |
| facebook/drama-1b-fp16                                           |     36.06 |                                71.07 |                            46.18 |                51.1  |     17 |
| upskyy/bge-m3-korean                                             |     22.08 |                                73.49 |                            32.66 |                42.74 |     18 |

# Retrieval
|                                                                  |   Ko-StrategyQA |   AutoRAGRetrieval |   PublicHealthQA |   XPQARetrieval |   facebook/belebele |   webfaq-retrieval |   Retrieval_Average |   Rank |
|:-----------------------------------------------------------------|----------------:|-------------------:|-----------------:|----------------:|--------------------:|-------------------:|--------------------:|-------:|
| dragonkue/snowflake-arctic-embed-l-v2.0-ko                       |           80.01 |              90.33 |            82.56 |           42.69 |               95.07 |              85.97 |               79.44 |      1 |
| Qwen/Qwen3-Embedding-8B-bf16                                     |           83.08 |              81.1  |            86.9  |           38.24 |               98.05 |              85.02 |               78.73 |      2 |
| FronyAI/frony-embed-medium-arctic-ko-v2.5                        |           79.46 |              90.42 |            81.61 |           37.77 |               92.9  |              85.03 |               77.86 |      3 |
| Qwen/Qwen3-Embedding-4B-bf16                                     |           81.98 |              82.38 |            85.88 |           37.9  |               94.12 |              83.83 |               77.68 |      4 |
| facebook/drama-1b-fp16                                           |           79.57 |              86.77 |            80.06 |           36.97 |               95.73 |              84.62 |               77.29 |      5 |
| nlpai-lab/KURE-v1                                                |           79.2  |              86.66 |            81.1  |           36.49 |               94.91 |              85.06 |               77.24 |      6 |
| Snowflake/snowflake-arctic-embed-l-v2.0                          |           79.57 |              83.61 |            80.78 |           41.33 |               92.51 |              85.44 |               77.21 |      7 |
| dragonkue/BGE-m3-ko                                              |           78.75 |              86.65 |            80.49 |           36.42 |               94.88 |              85.04 |               77.04 |      8 |
| nlpai-lab/KoE5                                                   |           78.85 |              84.46 |            83.68 |           34.73 |               94.2  |              84.17 |               76.68 |      9 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |           79.98 |              79.71 |            87.45 |           37.35 |               92.09 |              82.49 |               76.51 |     10 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |           80.29 |              75.12 |            80.93 |           39.86 |               94.56 |              83.6  |               75.73 |     11 |
| BAAI/bge-m3                                                      |           78.58 |              82.32 |            79.36 |           34.64 |               92.87 |              84.15 |               75.32 |     12 |
| FronyAI/frony-embed-medium-ko-v2                                 |           77.53 |              80.19 |            79.28 |           33.51 |               92.04 |              81.58 |               74.02 |     13 |
| intfloat/multilingual-e5-large-instruct                          |           79.59 |              74.56 |            81.35 |           31.46 |               91.76 |              81.69 |               73.4  |     14 |
| Qwen/Qwen3-Embedding-0.6B-bf16                                   |           75.85 |              81.83 |            78.59 |           31.92 |               91.66 |              79.96 |               73.3  |     15 |
| BAAI/bge-multilingual-gemma2-fp16                                |           78.2  |              75.64 |            65.6  |           37.08 |               95.79 |              82.14 |               72.41 |     16 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |           70.17 |              75.34 |            79.11 |           36.72 |               86.8  |              83.15 |               71.88 |     17 |
| upskyy/bge-m3-korean                                             |           74.2  |              71.66 |            76.53 |           30.27 |               86.91 |              80.28 |               69.98 |     18 |

# Task별 Query_fix / Instruction
|                                                                  | STS                                                                               | NLI                                                                                            | Clustering                                                                                     | IR                         |
|:-----------------------------------------------------------------|:----------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------|:---------------------------|
| BAAI/bge-m3                                                      |                                                                                   |                                                                                                |                                                                                                |                            |
| dragonkue/BGE-m3-ko                                              |                                                                                   |                                                                                                |                                                                                                |                            |
| upskyy/bge-m3-korean                                             |                                                                                   |                                                                                                |                                                                                                |                            |
| nlpai-lab/KoE5                                                   |                                                                                   |                                                                                                |                                                                                                |                            |
| nlpai-lab/KURE-v1                                                |                                                                                   |                                                                                                |                                                                                                |                            |
| FronyAI/frony-embed-medium-ko-v2                                 |                                                                                   |                                                                                                |                                                                                                | github issue 요청사항 적용 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |                                                                                   |                                                                                                |                                                                                                |                            |
| FronyAI/frony-embed-medium-arctic-ko-v2.5                        |                                                                                   |                                                                                                |                                                                                                | github issue 요청사항 적용 |
| Snowflake/snowflake-arctic-embed-l-v2.0                          | query:                                                                            | query:                                                                                         | query:                                                                                         | 허깅페이스 기준 적용       |
| dragonkue/snowflake-arctic-embed-l-v2.0-ko                       | query:                                                                            | query:                                                                                         | query:                                                                                         | 허깅페이스 기준 적용       |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        | (큰 차이는 없었음)None or Instruct: retrieve semantically similar text.<br>Query: |                                                                                                | Instruct: Identify the topic or theme of the given texts<br>Query:                             | 허깅페이스 기준 적용       |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           | Instruct: retrieve semantically similar text.<br>Query:                           | Instruct: retrieve semantically similar text.<br>Query:                                        | Instruct: Given a web search query, retrieve relevant passages that answer the query<br>Query: | 허깅페이스 기준 적용       |
| BAAI/bge-multilingual-gemma2-fp16                                | <instruct>retrieve semantically similar text.<br><query>                          | <instruct>retrieve semantically similar text.<br><query>                                       | <instruct>Identify the topic or theme of the given texts<br><query>                            | 허깅페이스 기준 적용       |
| intfloat/multilingual-e5-large-instruct                          | Instruct: retrieve semantically similar text.<br>Query:                           | Instruct: Determine whether the two given sentences express the same meaning or not.<br>Query: | Instruct: Identify the topic or theme of the given texts<br>Query:                             | 허깅페이스 기준 적용       |
| facebook/drama-1b-fp16                                           | Query:                                                                            | Query:                                                                                         | Query:                                                                                         | 허깅페이스 기준 적용       |
| Qwen3-Embedding                                                  | Instruct: retrieve semantically similar text.<br>Query:                           | Instruct: retrieve semantically similar text.<br>Query:                                        | Instruct: Given a web search query, retrieve relevant passages that answer the query<br>Query: | 허깅페이스 기준 적용       |

https://onand0n.github.io/ko-embedding-leaderboard/



