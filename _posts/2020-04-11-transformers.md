---
layout: post
title: "Transformers(Attention Is All You Need)"
---
## 원문
- <https://arxiv.org/abs/1706.03762>

## 왜 등장했을까?
- seq2seq 모델은 시계열(순서가 있는) 데이터를 다른 형태의 시계열 데이터로 변신시켜 준다.
- 기존 seq2seq 모델은 LSTM으로 구현되어 있는데, LSTM은 데이터를 순차적으로 처리하기 때문에 병렬화시킬 수 없다. 따라서 느리다.

![](/media/posts/transformers/seq2seq_lstm_encoder.svg)

## 전체 구조
- 인코더 + 디코더로 구성되며 구조적으로는 seq2seq 모델과 동일하다.

![](/media/posts/transformers/transformer_overview.svg)

## LSTM에서 어텐션으로
- LSTM을 사용하는 이유는 단어(그램) 간 거리에 따른 관계를 표현하기 위해서이다.
- 따라서 단어 간 거리에 따른 관계를 표현하는 다른 방법이 있다면 LSTM을 대체할 수 있다.
- 단어의 문장 내 위치를 나타내는 벡터를 이용하면, 단어 간 거리에 따른 관계를 계산할 수 있다. 트랜스포머는 이 방법(어텐션)을 사용하여 LSTM을 대체한다.
- 어텐션에서는 단어의 문장 내 위치를 나타내는 벡터를 구해서 입력 단어 벡터에 더해준다.

![](/media/posts/transformers/transformer_position_embedding.svg)

## 인코더의 셀프 어텐션
- 인코더는 입력된 문장 내 단어 간의 관계를 표현하기위해 위해 셀프 어텐션을 수행한다.
- 어텐션에서는 관계를 나타내고자 하는 단어 벡터를 query, 관계의 대상이 되는 단어 벡터들을 key와 value로 표현한다.
- 어텐션 수행 시, 단어 벡터를 그대로 사용하는 것이 아니라 Q, K, V에 매칭되는 가중치 행렬 W(Q), W(K), W(V)를 두고, 각 단어 벡터에 가중치를 곱해서 Q, K, V 값을 뽑아낸다.
- 가중치만 곱했을 뿐이므로 Q, K, V의 각 행은 각 단어를 표현하는 벡터라고 볼 수 있다.
- Q, K, V 값에 매칭되는 가중치 행렬은 어텐션을 수행할수록 학습된다.

![](/media/posts/transformers/transformer_self_attention_weight.svg)

- 각 단어 벡터에는 위치 벡터가 포함되어 있으므로, Q, K, V에도 단어의 위치 정보가 반영되어 있다.
- 따라서 Q와 K의 내적을 구하면 단어의 거리에 따른 관계를 계산할 수 있다. 계산 후에는 softmax를 적용해 관계를 확률로 나타내고 이 값을 다시 V에 곱해서 최종적으로 단어를 표현하는 벡터를 만든다. 단어 벡터들을 이어 붙여 문장 벡터를 만든다.
- 이 과정은 순서대로 진행되지 않아도 되므로, 병렬 처리가 가능하다.

![](/media/posts/transformers/transformer_self_attention.svg)

## 인코더
- 셀프 어텐션으로 문장 내 모든 단어의 관계를 구한 후, 결과 벡터를 입력 문장 벡터와 동일한 차원으로 만들어준다. 이후 각 단어의 위치 벡터 값이 소실되는 것을 막기 위해 입력 문장 벡터를 한번 더해준다. 여기까지가 어텐션 블럭이다.
- 어텐션 블럭의 결과 벡터를 완전 연결 피드 포워드 층에 통과시키고, 통과시킨 후에는 어텐션 블럭과 마찬가지로 입력 문장 벡터를 더해준다. 여기까지가 인코더 블럭이다.
- 총 6개의 인코더 블럭이 있으며, 인코더 블럭의 입/출력 벡터 모양이 같기 때문에 인코더 블럭을 쭉 이어 붙여 벡터를 통과시킬 수 있다. 인코더 블럭 6개를 통과한 벡터가 인코더의 최종 출력이 된다.

![](/media/posts/transformers/transformer_encoder.svg)

## 멀티 헤드 어텐션
- 셀프 어텐션 블럭을 병렬로 여러개 붙이면, 모호한 문장 내 각 단어 간 관계를 여러개의 어텐션 블럭으로 풍부하게 표현할 수 있기때문에 문맥을 보다 정밀하게 해석할 수 있다. 이를 멀티 헤드 어텐션이라고 하며, 총 8개의 헤드를 사용한다.

![](/media/posts/transformers/transformer_multihead_attention.svg)

## 디코더
- 디코더는 인코더와 동일한 구조이며, 셀프 어텐션과 어텐션. 두 부분만 다르다.
- 디코더를 통과시킨 후 얻은 벡터를 단어들의 확률로 나타내기 위해 linear와 softmax 층에 통과시킨다.
- softmax층을 통해 얻은 각 단어들의 확률 테이블에서 가장 높은 확률을 가진 단어를 선택하여 실제 단어로 표현한다.

![](/media/posts/transformers/transformer_decoder.svg)

## 디코더의 셀프 어텐션
- 디코더의 셀프 어텐션에서는 Q와 K의 내적을 구할 때, K 중에서 문장 내 단어 순서상 Q와 Q 이전에 출현했던 단어들의 벡터만 내적 대상에 포함시킨다(Q 뒤에 나오는 단어들은 마스킹한다.)

![](/media/posts/transformers/transformer_decoder_self_attention.svg)

## 디코더의 어텐션
- 디코더 어텐션에서는 실제로 입력 문장 내 단어들과 출력 문장 내 단어들 사이에 관계를 구한다.
- 동일하게 Q, K, V를 사용해 구하며 여기서 Q는 셀프 어텐션을 수행한 출력 문장 벡터를 사용해 뽑아내고, K, V는 인코더의 최종 출력 벡터를 가지고 뽑아낸다.
- Q와 K의 내적, 즉 입력 문장 내 단어들과 출력 문장 내 단어들 사이에 관계도를 구하는 것이 핵심이다.

![](/media/posts/transformers/transformer_decoder_attention.svg)

- 참조
	- <https://papers.nips.cc/paper/7181-attention-is-all-you-need.pdf>
	- <https://www.youtube.com/watch?v=mxGCEWOxfe8&t=581s>
	- <http://jalammar.github.io/illustrated-transformer/>
