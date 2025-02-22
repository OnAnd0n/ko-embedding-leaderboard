
# 한국어 오픈소스 임베딩 모델 리더보드
## ko-embedding-leaderboard

- IR / Clustering 평가 Dataset 추가 예정
- 평가 코드 업로드 예정
- HuggingFace에 기재된 대로 진행하되, SentenceTransformer > Transformers 의 우선순위로 모델 load.
  (단, Flagembedding으로만 기재된 경우, Transformers로 Load  //  Flagembedding로 Load 필요시, 추후 진행)
- pair sentence로 존재하는 Dataset 중, 중복 pair는 제거 ( (A, B) = (B, A) )
- LLM Based 임베딩 모델은 fp16/bf16으로 평가
- 문의 사항이나, 평가가 필요한 모델은 issue에 남겨주세요.
- 잘못된 부분에 대한 조언/멘트는 감사히 받겠습니다.

# 종합 순위
|                                                                  |   STS_Average |   NLI_Average |   Clustering_Average |   Retrieval_Average |   Average |   Rank |
|:-----------------------------------------------------------------|--------------:|--------------:|---------------------:|--------------------:|----------:|-------:|
| nlpai-lab/KURE-v1                                                |         83.37 |         64.79 |                39.21 |               82.93 |     67.58 |      1 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |         79.97 |         67.21 |                45.56 |               72.76 |     66.38 |      2 |
| BAAI/bge-m3                                                      |         83.46 |         65.32 |                33.01 |               80.45 |     65.56 |      3 |
| nlpai-lab/KoE5                                                   |         81.36 |         60.27 |                36.22 |               81.66 |     64.88 |      4 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |         78.04 |         63.55 |                40.05 |               77.71 |     64.84 |      5 |
| dragonkue/BGE-m3-ko                                              |         84.1  |         62.01 |                29.49 |               82.7  |     64.58 |      6 |
| upskyy/bge-m3-korean                                             |         84.67 |         70.82 |                22.08 |               72.93 |     62.62 |      7 |
| BAAI/bge-multilingual-gemma2-fp16                                |         80.12 |         65.89 |                26.97 |               76.92 |     62.47 |      8 |
| infloat/me5-instruct                                             |         82.24 |         63.17 |                26.62 |               77.08 |     62.28 |      9 |

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
| infloat/me5-instruct                                             |      85.65 |     79.43 |   81.65 |         82.24 |      5 |
| nlpai-lab/KoE5                                                   |      85.1  |     79.01 |   79.96 |         81.36 |      6 |
| BAAI/bge-multilingual-gemma2-fp16                                |      82.09 |     78.44 |   79.84 |         80.12 |      7 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |      80.81 |     78.79 |   80.3  |         79.97 |      8 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |      79.67 |     76.23 |   78.22 |         78.04 |      9 |


# NLI
|                                                                  |   KLUE-NLI |   Kor-NLI |   PawsX-PairClassification |   NLI_Average |   Rank |
|:-----------------------------------------------------------------|-----------:|----------:|---------------------------:|--------------:|-------:|
| upskyy/bge-m3-korean                                             |      75.72 |     84.5  |                      52.23 |         70.82 |      1 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |      68.29 |     80.78 |                      52.56 |         67.21 |      2 |
| BAAI/bge-multilingual-gemma2-fp16                                |      66.4  |     77.6  |                      53.66 |         65.89 |      3 |
| BAAI/bge-m3                                                      |      68.34 |     74.88 |                      52.75 |         65.32 |      4 |
| nlpai-lab/KURE-v1                                                |      67.34 |     75.12 |                      51.92 |         64.79 |      5 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |      59.75 |     75.03 |                      55.88 |         63.55 |      6 |
| infloat/me5-instruct                                             |      66.1  |     72.73 |                      50.68 |         63.17 |      7 |
| dragonkue/BGE-m3-ko                                              |      65.41 |     68.71 |                      51.92 |         62.01 |      8 |
| nlpai-lab/KoE5                                                   |      61.81 |     66.22 |                      52.79 |         60.27 |      9 |

# Clustering
|                                                                  |   sib2000 |   Clustering_Average |   Rank |
|:-----------------------------------------------------------------|----------:|---------------------:|-------:|
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |     45.56 |                45.56 |      1 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |     40.05 |                40.05 |      2 |
| nlpai-lab/KURE-v1                                                |     39.21 |                39.21 |      3 |
| nlpai-lab/KoE5                                                   |     36.22 |                36.22 |      4 |
| BAAI/bge-m3                                                      |     33.01 |                33.01 |      5 |
| dragonkue/BGE-m3-ko                                              |     29.49 |                29.49 |      6 |
| BAAI/bge-multilingual-gemma2-fp16                                |     26.97 |                26.97 |      7 |
| infloat/me5-instruct                                             |     26.62 |                26.62 |      8 |
| upskyy/bge-m3-korean                                             |     22.08 |                22.08 |      9 |

# Retrieval
|                                                                  |   Ko-StrategyQA |   AutoRAGRetrieval |   Retrieval_Average |   Rank |
|:-----------------------------------------------------------------|----------------:|-------------------:|--------------------:|-------:|
| nlpai-lab/KURE-v1                                                |           79.2  |              86.66 |               82.93 |      1 |
| dragonkue/BGE-m3-ko                                              |           78.75 |              86.65 |               82.7  |      2 |
| nlpai-lab/KoE5                                                   |           78.85 |              84.46 |               81.66 |      3 |
| BAAI/bge-m3                                                      |           78.58 |              82.32 |               80.45 |      4 |
| Alibaba-NLP/gte-Qwen2-7B-instruct-fp16                           |           80.29 |              75.12 |               77.71 |      5 |
| infloat/me5-instruct                                             |           79.59 |              74.56 |               77.08 |      6 |
| BAAI/bge-multilingual-gemma2-fp16                                |           78.2  |              75.64 |               76.92 |      7 |
| upskyy/bge-m3-korean                                             |           74.2  |              71.66 |               72.93 |      8 |
| McGill-NLP/LLM2Vec-Meta-Llama-3-8B-Instruct-mntp-supervised-bf16 |           70.17 |              75.34 |               72.76 |      9 |



