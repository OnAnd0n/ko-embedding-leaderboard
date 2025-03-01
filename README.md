
# 한국어 오픈소스 임베딩 모델 리더보드
## ko-embedding-leaderboard

- MTEB를 custom하여 오픈소스 임베딩 모델을 평가 (데이터셋 일부 수정)
- 평가 코드 업로드 예정
- IR / Clustering 평가 Dataset 추가 예정
- HuggingFace에 기재된 대로 진행하되, SentenceTransformer > Transformers 의 우선순위로 모델 load.
  (단, Flagembedding으로만 기재된 경우, SentenceTransformer와 Transformers 중 높은 성능의 것으로 기입  //  Flagembedding로 Load 필요시, 추후 진행)
- pair sentence로 존재하는 Dataset 중, 중복 pair는 제거 ( (A, B) = (B, A) )
- LLM Based 임베딩 모델은 fp16/bf16으로 평가
- 문의 사항이나, 평가가 필요한 모델은 issue에 남겨주세요.
- 잘못된 부분에 대한 조언/멘트는 감사히 받겠습니다.

평가 방식 살펴보기 : [MTEB 코드 살펴보기 (2)](https://introduce-ai.tistory.com/entry/%EC%9E%84%EB%B2%A0%EB%94%A9-%EB%AA%A8%EB%8D%B8-%ED%8F%89%EA%B0%80-MTEB-%EC%BD%94%EB%93%9C-%EC%82%B4%ED%8E%B4%EB%B3%B4%EA%B8%B0-2-Custom-Model-%ED%8F%89%EA%B0%80) 


### 평가 Metric
- STS : mean of {pearson, spearman, cosine_pearson, cosine_spearman, ..., euclidean_spearman}
- NLI : average precision
- Clustering : v-measure
- Retrieval : mean of NDCG @ 5, 10
- Weighted_Average => Retrieval : 50%,  [Clustering, NLI, STS] : 50%

# 종합 순위
|                                                                  |   STS_Average |   NLI_Average |   Clustering_Average |   Retrieval_Average |   Weighted_Average |   Rank |
|:-----------------------------------------------------------------|--------------:|--------------:|---------------------:|--------------------:|-------------------:|-------:|
| nlpai-lab/KURE-v1                                                |         83.37 |         64.79 |                39.21 |               70.86 |              66.66 |      1 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |         83.09 |         66.86 |                32.71 |               71.12 |              66    |      2 |
| nlpai-lab/KoE5                                                   |         81.36 |         60.27 |                36.22 |               70.43 |              64.86 |      3 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |         78.04 |         63.55 |                40.05 |               69.05 |              64.8  |      4 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |         79.97 |         67.21 |                45.56 |               65.34 |              64.79 |      5 |
| BAAI/bge-m3                                                      |         83.46 |         65.32 |                33.01 |               68.72 |              64.66 |      6 |
| dragonkue/BGE-m3-ko                                              |         84.1  |         62.01 |                29.49 |               70.58 |              64.56 |      7 |
| infloat/me5-instruct                                             |         82.24 |         63.17 |                26.62 |               66.74 |              62.04 |      8 |
| upskyy/bge-m3-korean                                             |         84.67 |         70.82 |                22.08 |               63.17 |              61.18 |      9 |
| BAAI/bge-multilingual-gemma2-fp16                                |         80.12 |         65.89 |                26.97 |               64.13 |              60.9  |     10 |
| facebook/drama-1b-fp16                                           |         77.24 |         60.32 |                36.09 |              nan    |             nan    |     11 |

#
#
#

# STS
|                                                                  |   KLUE-STS |   Kor-STS |   STS17 |   STS_Average |   Rank |
|:-----------------------------------------------------------------|-----------:|----------:|--------:|--------------:|-------:|
| upskyy/bge-m3-korean                                             |      86.73 |     82.82 |   84.45 |         84.67 |      1 |
| dragonkue/BGE-m3-ko                                              |      87.35 |     81.76 |   83.19 |         84.1  |      2 |
| BAAI/bge-m3                                                      |      86.8  |     80.98 |   82.59 |         83.46 |      3 |
| nlpai-lab/KURE-v1                                                |      87.48 |     80.97 |   81.67 |         83.37 |      4 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |      85.32 |     81.25 |   82.71 |         83.09 |      5 |
| infloat/me5-instruct                                             |      85.65 |     79.43 |   81.65 |         82.24 |      6 |
| nlpai-lab/KoE5                                                   |      85.1  |     79.01 |   79.96 |         81.36 |      7 |
| BAAI/bge-multilingual-gemma2-fp16                                |      82.09 |     78.44 |   79.84 |         80.12 |      8 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |      80.81 |     78.79 |   80.3  |         79.97 |      9 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |      79.67 |     76.23 |   78.22 |         78.04 |     10 |
| facebook/drama-1b-fp16                                           |      82.7  |     74.41 |   74.62 |         77.24 |     11 |


# NLI
|                                                                  |   KLUE-NLI |   Kor-NLI |   PawsX-PairClassification |   NLI_Average |   Rank |
|:-----------------------------------------------------------------|-----------:|----------:|---------------------------:|--------------:|-------:|
| upskyy/bge-m3-korean                                             |      75.72 |     84.5  |                      52.23 |         70.82 |      1 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |      68.29 |     80.78 |                      52.56 |         67.21 |      2 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |      69.16 |     78.84 |                      52.58 |         66.86 |      3 |
| BAAI/bge-multilingual-gemma2-fp16                                |      66.4  |     77.6  |                      53.66 |         65.89 |      4 |
| BAAI/bge-m3                                                      |      68.34 |     74.88 |                      52.75 |         65.32 |      5 |
| nlpai-lab/KURE-v1                                                |      67.34 |     75.12 |                      51.92 |         64.79 |      6 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |      59.75 |     75.03 |                      55.88 |         63.55 |      7 |
| infloat/me5-instruct                                             |      66.1  |     72.73 |                      50.68 |         63.17 |      8 |
| dragonkue/BGE-m3-ko                                              |      65.41 |     68.71 |                      51.92 |         62.01 |      9 |
| facebook/drama-1b-fp16                                           |      62.29 |     68.14 |                      50.52 |         60.32 |     10 |
| nlpai-lab/KoE5                                                   |      61.81 |     66.22 |                      52.79 |         60.27 |     11 |

# Clustering
|                                                                  |   sib2000 |   Clustering_Average |   Rank |
|:-----------------------------------------------------------------|----------:|---------------------:|-------:|
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |     45.56 |                45.56 |      1 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |     40.05 |                40.05 |      2 |
| nlpai-lab/KURE-v1                                                |     39.21 |                39.21 |      3 |
| nlpai-lab/KoE5                                                   |     36.22 |                36.22 |      4 |
| facebook/drama-1b-fp16                                           |     36.09 |                36.09 |      5 |
| BAAI/bge-m3                                                      |     33.01 |                33.01 |      6 |
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |     32.71 |                32.71 |      7 |
| dragonkue/BGE-m3-ko                                              |     29.49 |                29.49 |      8 |
| BAAI/bge-multilingual-gemma2-fp16                                |     26.97 |                26.97 |      9 |
| infloat/me5-instruct                                             |     26.62 |                26.62 |     10 |
| upskyy/bge-m3-korean                                             |     22.08 |                22.08 |     11 |

# Retrieval
|                                                                  |   Ko-StrategyQA |   AutoRAGRetrieval |   PublicHealthQA |   XPQARetrieval |   Retrieval_Average |   Rank |
|:-----------------------------------------------------------------|----------------:|-------------------:|-----------------:|----------------:|--------------------:|-------:|
| kakaocorp/kanana-nano-2.1b-embedding-fp16                        |           79.98 |              79.71 |            87.45 |           37.35 |               71.12 |      1 |
| nlpai-lab/KURE-v1                                                |           79.2  |              86.66 |            81.1  |           36.49 |               70.86 |      2 |
| dragonkue/BGE-m3-ko                                              |           78.75 |              86.65 |            80.49 |           36.42 |               70.58 |      3 |
| nlpai-lab/KoE5                                                   |           78.85 |              84.46 |            83.68 |           34.73 |               70.43 |      4 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |           80.29 |              75.12 |            80.93 |           39.86 |               69.05 |      5 |
| BAAI/bge-m3                                                      |           78.58 |              82.32 |            79.36 |           34.64 |               68.72 |      6 |
| infloat/me5-instruct                                             |           79.59 |              74.56 |            81.35 |           31.46 |               66.74 |      7 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |           70.17 |              75.34 |            79.11 |           36.72 |               65.34 |      8 |
| BAAI/bge-multilingual-gemma2-fp16                                |           78.2  |              75.64 |            65.6  |           37.08 |               64.13 |      9 |
| upskyy/bge-m3-korean                                             |           74.2  |              71.66 |            76.53 |           30.27 |               63.17 |     10 |
| facebook/drama-1b-fp16                                           |                 |                    |                  |                 |                     |     11 |



