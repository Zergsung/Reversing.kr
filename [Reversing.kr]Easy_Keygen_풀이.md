# [Reversing.kr] Easy Keygen 풀이

Created: 2022년 11월 25일 오후 10:22
Tags: Rev

압축을 풀면 Readme.txt라는 파일에 이렇게 써져있다.

![Untitled](/IMG/EasyKeygen/EasyKeygen.png)

어떤네임을 입력하면 저 시리얼키랑 일치하는지 알아내는 문제같다.

![Untitled](/IMG/EasyKeygen/EasyKeygen1.png)

실행시켜보면 위와같이 된다.

![Untitled](/IMG/EasyKeygen/EasyKeygen2.png)

프로그램은 32비트이다.

![Untitled](/IMG/EasyKeygen/EasyKeygen3.png)

입력한 name이 어떤 알고리즘으로 시리얼키가 생성이 되는지 알기위해 브레이크포인트를 걸고 디버깅을 해보겠다.

![Untitled](/IMG/EasyKeygen/EasyKeygen4.png)

위부분을 보면 내가 입력한 값이 esp+18에 위치하는것을 알 수 있다.

![Untitled](/IMG/EasyKeygen/EasyKeygen5.png)

위 코드에서 보면 esp+esi+C에는 0x10,0x20,0x30이 들어가있고 esp+ebp+10에는 내가 입력한값이 들어가 있는것을 확인할수있다. 그리고 아래에는 그 값끼리 xor연산을 하는걸 볼 수 있다. 이부분에서 어떤식으로 시리얼키가 생성이 되는지 감이 잡혔다. 

![Untitled](/IMG/EasyKeygen/EasyKeygen6.png)

![Untitled](/IMG/EasyKeygen/EasyKeygen7.png)

만약에 내가 aaaa를 입력하면 첫번째 a부터 0x10이랑 xor연산을 한값을 시리얼키로 받는거같다. 그리고 0x10부터 0x30까지 3번 xor을 끝내면 다시 0x10으로 돌아가서 연산을 해서 키가 만들어지는걸 알 수 있다.

xor연산의 특징으로는 A ^ B = C  면 A = B ^ C 가 성립이 된다는 것이다. 그럼 Readme파일에서 준 값을 0x10,0x20,0x30으로 연산을 해주면 플래그를 얻을 수 있다.  코드를 짜보자.

### 파이썬코드

```python
serial = [0x5B, 0x13, 0x49, 0x77, 0x13, 0x5E, 0x7D, 0x13]
xor = [0x10, 0x20, 0x30]
count = 0

for i in range(0,len(serial)):
  if count == 2:
    print(chr(serial[i] ^ xor[count]), end = "")
    count = 0

  else:
    print(chr(serial[i] ^ xor[count]),end="")
    count += 1
```

코드를 짜고 실행해보니 플래그가 나왔다.

![Untitled](/IMG/EasyKeygen/EasyKeygen8.png)