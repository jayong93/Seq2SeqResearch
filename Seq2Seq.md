# Sequence To Sequence

seq2seq 모델은 Encoder와 Decoder 2개의 모듈을 가지는 RNN 모델이라고 볼 수 있다.

Encoder와 Decoder의 입력, Decoder의 출력은 모두 Embedding 되어 있어야 한다.

## Encoder
Encoder는 Text Classification과 유사한 모양새를 가졌는데, 시간 순서로 나열되어 있는 입력을 RNN Cell로 읽어서 처리한다. 하지만 Decoder가 Plain Decoder인 경우엔 Encoder의 각 단계 출력은 무시된다.

입력 토큰이 들어올 때 마다 내부 상태값이 바뀌고 마지막 토큰이 들어온 뒤에는 내부 상태값이 입력 토큰들에 대한 데이터를 모두 가지고 있게 된다.

## Decoder
Decoder는 Output을 만들어내는 모듈로 Encoder의 처리가 끝난 뒤에 시작된다. Encoder의 최종 내부 상태와 End Token을 이용해서 출력값을 만들어낸다.

학습할 때는 미리 만들어진 Decoder input을 이용하고, 실제 추론에서는 각 Decoder 단계의 출력이 다음 단계의 입력으로 들어가게 된다. Tensorflow에는 학습단계에서 Decoder input을 이용하기 위한 TrainingHelper와 추론에서 사용할 GreedyEmbeddingHelper가 존재한다.

Attention vector를 이용한 Attention Decoder의 경우엔 Decoder의 hidden state를 이용해서 Encoder의 각 단계 출력으로부터 정보를 뽑아낸다. 이렇게 하면 Decoder의 출력들이 Encoder의 각 입력들과 비슷한 경향을 띄도록 만들 수 있다.