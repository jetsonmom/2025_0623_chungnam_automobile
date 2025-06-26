Python에서 주의해야 할 점들

- 문법 관련 주의사항

- 들여쓰기 (Indentation)

- Python은 들여쓰기로 코드 블록을 구분합니다

- 탭과 스페이스를 섞어 쓰면 안 됩니다

- 일관성 있게 스페이스 4개 또는 탭 사용

   ![image](https://github.com/user-attachments/assets/8686a8a1-0bb8-4812-a8ac-d79c685bff2e)


 대소문자 구분
- Python은 대소문자를 구분합니다
- Print와 print는 완전히 다른 것
   ![image](https://github.com/user-attachments/assets/7cf99bac-2547-4476-9239-ea6bdad77d6b)


변수와 데이터 타입
### 변수명 규칙
- 숫자로 시작할 수 없음
- 특수문자 사용 불가 (밑줄 _ 제외)
- 예약어 사용 불가

  ![image](https://github.com/user-attachments/assets/dacf6292-bb80-44da-b05f-fff67cf9dba9)

- 문자열 처리 주의사항
  ![image](https://github.com/user-attachments/assets/7d15fb9d-3a1b-49f3-ba09-dea56de1ce15)



리스트와 인덱스
- 인덱스 범위 주의

| 코드 | 결과 | 설명 |
|:-----|:-----|:-----|
| `my_list = [1, 2, 3]` | 리스트 생성 | 인덱스 0, 1, 2를 가진 리스트 |
| `print(my_list[3])` | IndexError | 에러! 인덱스 범위 초과 (인덱스 3은 존재하지 않음) |
| `print(my_list[2])` | `3` | 올바름 (마지막 요소, 인덱스 2) |
| `print(my_list[-1])` | `3` | 올바름 (뒤에서 첫 번째 요소) |

- 리스트 복사 주의

  
| 코드 | 결과 | 설명 |
|:-----|:-----|:-----|
| `list1 = [1, 2, 3]` | 리스트 생성 | 원본 리스트 생성 |
| `list2 = list1` | 참조 복사 | 같은 메모리를 가리킴 (얕은 복사) |
| `list2.append(4)` | list2에 4 추가 | list1과 list2가 같은 객체이므로 둘 다 변경됨 |
| `print(list1)` | `[1, 2, 3, 4]` | 원본도 변경됨! list2 변경이 list1에도 영향




함수 관련
- 매개변수 기본값 주의
- 위험한 코드

def add_item(item, my_list=[]):
    my_list.append(item)
    return my_list
```

- 문제: 기본값이 공유됨

```
list1 = add_item("apple")
list2 = add_item("banana")
print(list2)  # ['apple', 'banana'] - 예상과 다름!
```
- 올바른 코드
  ```
def add_item(item, my_list=None):
    if my_list is None:
        my_list = []
    my_list.append(item)
    return my_list
```
예외 처리
예외 처리 습관화
- 위험한 코드
```
number = int(input("숫자 입력: "))  # 문자 입력 시 에러!
```
# 안전한 코드

try:
    number = int(input("숫자 입력: "))
    result = 10 / number
    print(f"결과: {result}")
except ValueError:
    print("숫자를 입력해주세요")
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다")

파일 처리
파일을 열었으면 반드시 닫아야 합니다!
파일 닫기 잊지 말기
- 위험한 코드
file = open("data.txt", "r")
data = file.read()
# file.close() # 파일을 닫지 않음 ← 문제!

- 안전한 코드
with문 사용 (권장), 자동으로 파일이 닫힘

```
with open("data.txt", "r") as file:
    data = file.read()
```

성능 관련
문자열 연결 최적화


| 구분 | 코드 | 설명 |
|:-----|:-----|:-----|
| 비효율적 | `result = ""` | 빈 문자열로 초기화 |
| 비효율적 | `for i in range(1000):` | 반복문 시작 |
| 비효율적 | `result += str(i)` | 매번 새로운 문자열 객체 생성 (메모리 낭비) |
| 효율적 | `result = "".join(str(i) for i in range(1000))` | 한 번에 모든 문자열을 결합 (메모리 효율적) |

- 비효율적
result = ""
for i in range(1000):
    result += str(i)  # 매번 새로운 문자열 객체 생성

# 효율적
result = "".join(str(i) for i in range(1000))

일반적인 실수들
print문에서 괄호 빠뜨리기
# Python 2 스타일 (에러!)
print "Hello"

# Python 3 스타일 (올바름)
print("Hello")

들여쓰기 혼용
# 에러 발생하는 코드
if True:
    print("Hello")  # 스페이스 4개
	print("World")  # 탭 문자 - 에러!

전역변수 사용 주의
count = 0

def increment():
    global count  # global 키워드 필요
    count += 1

def increment_wrong():
    count += 1  # 에러! 지역변수로 인식

이런 점들을 주의하면서 코딩하면 Python을 더 안전하고 효율적으로 사용할 수 있어요!


