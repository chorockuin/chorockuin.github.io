---
layout: post
title: "NLP Dataset"
---
## 자연어 처리 데이터셋이란?
- 자연어 처리 알고리즘을 개발할 때 학습/검증/테스트용으로 사용하는 데이터이다.
- 보통 알고리즘을 개발하려는 목적 Task에 따라 데이터셋을 만들기 때문에 Task 이름으로 대충 부르기도 한다. 영어의 경우 공개 데이터셋이 많다.
	- *CoLA, SST-2, MRPC, SQuAD, ...*

## GLUE Task의 데이터셋
- CoLA(The Corpus of Linguistic Acceptability)
	- 책
	- (문장, 레이블)로 구성되며, 문장이 문법적으로 적절한지 레이블링(적절, 부적절)
	- MCC(Matthews Correlation Coefficient)
	- <https://nyu-mll.github.io/CoLA/>

- SST-2(The Stanford Sentiment Treebank)
	- 영화리뷰
	- (문장, 레이블)로 구성되며, 문장이 긍정적인지 부정적인지 레이블링(긍정,부정)
	- 정확도(accuracy)
	- <https://nlp.stanford.edu/sentiment/index.html>

- MPRC(Microsoft Research Paraphrase Corpus)
	- 뉴스
	- (문장1, 문장2, 레이블)로 구성되며, 두 문장이 의미적으로 동일한지 레이블링(동일, 상이)
	- f1 점수와 정확도(accuracy)
	- <https://www.microsoft.com/en-us/download/details.aspx?id=52398>

- STS-B(The Semantic Textual Similarity Benchmark)
	- 뉴스 헤드라인, 비디오나 이미지에 달린 문구, 사용자 포럼의 글
	- (문장1, 문장2, 레이블)로 구성되며, 두 문장이 의미적으로 비슷한지 레이블링(0.0점에서 5.0점 사이)
	- PSC(Pearson and Spearman Correlation)
	- <http://ixa2.si.ehu.es/stswiki/index.php/STSbenchmark>

- QQP(Quora Question Pairs)
	- Q&A 사이트인 Quora
	- (질문문장1, 질문문장2, 레이블)로 구성되며, 두 문장이 의미적으로 비슷한지 레이블링(동일, 상이)
	- f1 점수와 정확도(accuracy)
	- <https://www.quora.com/q/quoradata/First-Quora-Dataset-Release-Question-Pairs>

- MNLI(Multi-Genre Natural Language Inference)
	- 다양한 장르(소설, 편지, 전화 대화, 리포트 등) 문서
	- (전제문장, 추론문장, 레이블)로 구성되며, 전제문장에서 추론문장이 추론되는지 레이블링(추론,반대,중립)
	- 정확도(accuracy)
	- <https://www.nyu.edu/projects/bowman/multinli/>

- SQuAD(The Stanford Question Answering Dataset)
	- 위키피디아
	- (답을 포함한 문단, 질문문장, 레이블)로 구성되며 질문문장에 대한 답을 레이블링(문단 내 답의 위치)
	- 정확도(accuracy)
	- <https://rajpurkar.github.io/SQuAD-explorer/>

- QNLI(Question-answering Natural Language Inference)
	- SQuAD를 조금 수정
	- (답을 포함한 문단, 질문문장, 레이블)로 구성되며, 문단에 질문문장에 대한 답이 있는지 없는지 레이블링(있다, 없다)
	- 정확도(accuracy)
	- <https://rajpurkar.github.io/SQuAD-explorer/>

- RTE(Recognizing Textual Entailment)
	- 위키피디아
	- (전제문장, 추론문장, 레이블)로 구성되며, 전제문장에서 추론문장이 추론되는지 레이블링(추론,추론안됨)
	- 정확도(accuracy)
	- <https://aclweb.org/aclwiki/Recognizing_Textual_Entailment>

- WNLI(Winograd Natural Language Inference)
	- 소설책
	- (대명사를 포함한 문장, 대명사가 가리키는 대상 지칭, 레이블)로 구성되며, 대상 지칭이 적절한지 레이블링(적절, 부적절)
	- 정확도(accuracy)
	- <https://cs.nyu.edu/faculty/davise/papers/WinogradSchemas/WS.html>
