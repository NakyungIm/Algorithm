# Programmers Level 1 - 체육복

[**문제 링크**](https://programmers.co.kr/learn/courses/30/lessons/42862)


**입력**

- 전체 학생 수 n
- 도난 학생 번호 배열 lost
- 여벌 학생 번호 배열 reserve


**출력**

- 체육 수업 듣는 학생의 최대값


**풀이**

- lost와 reserve에 중복되는 사람 있으면 제거
(본인은 체육 수업 참여 가능. 하지만 체육복은 1개이기 때문에 남에게 빌려줄 수는 없음)
- lost를 기준으로 앞에서 부터 체육복 빌려줄 수 있는 사람 찾기


```python
def solution(n, lost, reserve):
    # answer 초기화
    answer = n - len(lost)

    # 두 리스트 같은 값 찾기. 있으면 제거
    lst = list(set(lost).intersection(reserve))
    for i in lst:
        answer += 1
        del lost[lost.index(i)]
        del reserve[reserve.index(i)]

    for i in lost:
        try: # 앞번호 학생이 reserve에 있는 경우
            reserve.index(i-1) != -1
            tmp = reserve.index(i-1)
            answer += 1
            del i
            del reserve[tmp]
        except:
            pass
        
        try: # 뒷번호 학생이 reserve에 있는 경우
            reserve.index(i+1) != -1
            tmp = reserve.index(i+1)
            answer += 1
            del i
            del reserve[tmp]
        except:
            pass
		
    return answer
```