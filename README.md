# Seq2Seq를 사용한 한국어-영어 구어체 번역 프로그램💻
`colab` 환경에서 작성된 코드입니다.

## 1. 프로젝트 소개👩‍🏫 
* 인코더-디코더 구조의 가장 기본적인 신경망인 `seq2seq`를 사용한 한국어-영어 번역 프로그램입니다.
* 논문을 통해 코드를 구현하고, 어텐션 매커니즘, 트랜스포머를 순차적으로 사용하여 성능 개선을 직접 눈으로 살펴보고, 원인을 분석해보는 것이 목표입니다.

### 🌟 특이사항
* 긴 코퍼스에 약한 seq2seq의 특징을 고려하여 비교적 문장의 길이가 짧은 구어체 말뭉치를 사용했습니다.
* `BucketIterator`를 통해 비슷한 길이의 시퀀스끼리 같은 배치에 묶이도록 했습니다.
* 최고 성능 모델을 저장하여 실시간으로 실행시켜 결과를 살펴볼 수 있는 코드를 추가하였습니다.([나동빈님의 코드 참고](https://github.com/ndb796/Deep-Learning-Paper-Review-and-Practice/blob/master/code_practices/Sequence_to_Sequence_with_LSTM_Tutorial.ipynb))

### 📃 데이터셋
* AI hub 한국어-영어 번역(병렬) 말뭉치-구어체(https://aihub.or.kr/aidata/87)
* 20만개 데이터셋
  * 학습 데이터셋: 180,000
  * 검증 데이터셋: 10,000
  * 테스트 데이터셋: 10,000

### ⚙ Settings
* Batch size: 256
* Epochs: 20

## 2. 실행 결과
![image](https://user-images.githubusercontent.com/74829786/164406902-6b9c8970-9359-4172-9c5d-472781c879e2.png)

## 3. 결과 분석
* 시퀀스가 길어질수록 the/is와 같은 빈도가 높지만 의미는 없는 단어들의 반복이 심해졌다.
  * 문장에서 중요한 단어를 잘 찾지 못함
  * `Attention`을 사용하여 성능 개선을 기대해볼 수 있음
* 문장에 포함되는 핵심 단어는 잘 가져왔지만 의미가 전혀 다르게 번역되었다.
  * 에폭 수를 늘려서 학습을 진행해본다.
## 4. Reference
* 결과 실행 코드: https://github.com/ndb796/Deep-Learning-Paper-Review-and-Practice/blob/master/code_practices/Sequence_to_Sequence_with_LSTM_Tutorial.ipynb
* BucketIterator 사용법: https://gmihaila.medium.com/better-batches-with-pytorchtext-bucketiterator-12804a545e2a
* https://pytorch.org/tutorials/intermediate/seq2seq_translation_tutorial.html
