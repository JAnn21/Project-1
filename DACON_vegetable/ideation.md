# 개요

## 목적
- 예측일 하루 전 자정까지 얻을 수 있는 데이터를 이용해 21개 품목 및 품종의 1주 후, 2주 후, 4주 후 가격을 예측한다.
    + 품목 및 품종: 배추, 무, 양파, 건고추, 마늘, 대파, 얼갈이 배추, 양배추, 깻잎, 시금치, 미나리, 당근, 파프리카, 새송이, 팽이버섯, 토마토, 청상추, 백다다기, 애호박, 캠벨얼리, 샤인머스캣

- 예측 대상: 2020년 10월 6일(화) ~ 2020년 11월 12일(목) 기간 내 품목별 1주, 2주, 4주 후 가격 

## 가격 산출 기준
- 전국 도매시장(총 거래금액) / (총 거래량) (원/kg)

## 모델 평가 산식
- NMAE(Normalized Mean Absolute Error)

```python
def nmae(answer_df, submission_df):
    answer = answer_df.iloc[:, 1:].to_numpy()
    submission = submission_df.iloc[:, 1:].to_numpy()
    target_idx = np.where(answer != 0)

    true = answer[target_idx]
    pred = submission[targert_idx]

    score = np.mean(np.abs(true - pred) / true)
    return score
```

# ideation

## 농산물의 가격에 영향을 미치는 변수는 어떤 것이 있을까?

- 수요의 변화
    + 인기의 변화 (샤인 머스캣과 같은 품종은 인기에 따라 수요가 달라질 수 있지 않을까?)
    + 명절로 인한 수요의 상승 (하지만 추석은 9.19 ~ 9.22로 예측 시기에서 벗어난다.)
    + 코로나19로 인해 학교/식당 등 대형 소비처에 대한 수요 변화   


- 공급의 변화
    + 기상이변 or 풍작
    + 농작물 전염병
    + 특정 시기에만 수확되는 농작물
    + 해외 농작물의 수입 or 해외로 농작물 수출

 
- 그 외 요인
    + 인건비/배송비/연료비의 변화
    + 물가 상승


## 데이터에서 보고 싶은 것

- 추세성이 있는가?
- 주기성이 있는가?

## 시계열 데이터 모델들
- prophet
- ARIMA
- RNN & LSTM & GRU

- 참고: https://www.kaggle.com/andreshg/timeseries-analysis-a-complete-guide
- https://www.kaggle.com/charel/learn-by-example-rnn-lstm-gru-time-series
