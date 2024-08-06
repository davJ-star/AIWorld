# 컴퓨터 비전에서 객체 감지
### 키워드
위치감지(Localistation)와 분류(classification)
![alt text](image-2.png)

### 객체 감지 방법: one vs two stage

![alt text](image.png)
![alt text](image-1.png)

### 그외 세그멘테이션
![alt text](image-3.png)

## IoU(Intersection of unionIoU)
어떻게 잘찾았다고 할것인가에대한 지표가 필요
![alt text](image-4.png)

IoU값은 0~1사이의 값을 가지며 완전히 겹칠때1, 겹치지 않을때 0값을 가짐

### 예측 & 재현 계산

Precision = (TP)/(TP+FP+FN)
Recall = (TP)/(TP+FP+FN+TN)

TP: True Positive, FP: False Positive, FN: False Negative

(뒤에가 검출 성공 여부(클래스), 앞에가 정답 여부(IOU))


## mAP(Mean Average Precision)
알고리즘의성능지표정하기
- 어떤지표를사용해야할까?(IOU를 넘어 전반적 파악)
![alt text](image-5.png)
- 성능이라는것을어떤것을고려해야할까?
![alt text](image-6.png)
![alt text](image-7.png)

        누가더예측을잘했을까?
    1. 헬멧만보고사람이라고맞춘알고리즘이맞는것일까?
    2. 알맞게사람이있는영역을찾았지만사람대신고양이라고판별한것이맞을까
    3. 시험문제의공정성, IoU기준이다르면?
    4. 시험문제의공정성, 신뢰도기준이다르면?
![alt text](image-8.png)


- 좋은성능지표를내려면고려해야하는것들
  ![alt text](image-9.png)
  ![alt text](image-10.png)
    신뢰도역치값에따라변하는Recall에따른Precision의값의평균= PR 곡선아래의면적
- D
  ![alt text](image-11.png)
    - TP ➡Positive으로응답(알고리즘이검출)IoU를역치를만족하고, 분류또한정답(True)
    - FP ➡Positive으로응답(알고리즘이검출)했으나IoU를역치를만족하지못하여틀린답(False)
    - FN ➡Negative으로응답(알고리즘이검출할게없다고답함)알고리즘이타겟을놓침(검출하지못함)
    - FN➡IoU를만족시켰으나Negative(Cat으로응답)으로응답분류가잘못됨
    - TN ➡Negative으로응답(검출할게없다고답함). 실제로도그곳은물체가없기때문에정답임(True)
- AP를구해봅시다.
  ![alt text](image-12.png)
  ![alt text](image-13.png)

  ![alt text](image-14.png)
  ![alt text](image-15.png)

- 다양한 클래스 고려
    예제에서는클래스하나(person)에대해서만Average Precision을구한것임•하지만실제로는클래스가여러개있으므로각클래스별Average Precision을구한다음에이들을평균한값인mAP값을통해성능을판단
    ![alt text](image-16.png)
- ㅇ
## NMS(Non-Max Suppression)
1. 너무 예측 결과가 많은 경우, 점수가 높은 박스들 순으로 정렬후, Threshold걸기
![alt text](image-17.png)

![alt text](image-18.png)
![alt text](image-19.png)

2. 최고점수bbox와다른bbox의IoU비교
   ![alt text](image-20.png)
3. NMS의결과후, 후처리(이해x)
   ![alt text](image-21.png)
