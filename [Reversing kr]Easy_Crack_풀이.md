# [Reversing.kr] Easy Crack 풀이

Created: 2022년 11월 25일 오전 1:24
Tags: Rev

---

![실행시켜서 abcd를 입력하고 확인을 누른 모습](/Reversing.kr/IMG/Easycrack/Easycrack.png)

실행시켜서 abcd를 입력하고 확인을 누른 모습

![문자열 참조로 'Incorrect Password'를 찾아보자](/Reversing.kr/IMG/Easycrack/Easycrack1.png)

문자열 참조로 'Incorrect Password'를 찾아보자

![매우 수상해 보이는 문자열이 있다.](/Reversing.kr/IMG/Easycrack/Easycrack2.png)

매우 수상해 보이는 문자열이 있다.

Incorrect Password 부분을 더블클릭해서 위치로 가보자~

![위치로 가고 위로 좀 올려보았다.](/Reversing.kr/IMG/Easycrack/Easycrack3.png)

위치로 가고 위로 좀 올려보았다.

커서가 있는 첫번재 cmp부분에 브레이크포인트를 걸고 실행시켜보겠다.

![abcd를 입력했다.](/Reversing.kr/IMG/Easycrack/Easycrack4.png)

abcd를 입력했다.

a랑 비교하는 esp+5에 어떤 글자가 있는지 확인하기 위해 덤프로 따라가보았다.

![내가 입력한게 있는모습](/Reversing.kr/IMG/Easycrack/Easycrack5.png)

내가 입력한게 있는모습

b랑 비교를 하는걸 보니 시리얼키의 두번째 글자는 a인가보다.

옆에 부분을 보니 너무 시리얼키인것처럼 문자열이 있었다.

![Untitled](/Reversing.kr/IMG/Easycrack/Easycrack6.png)

그래서 일단 a5yR3versing 까지는 알았는데 첫번째 글자가 뭔지 몰라서 살펴보던중

![Untitled](/Reversing.kr/IMG/Easycrack/Easycrack7.png)

분기점 바로전에서 E를 비교하는걸로보아 첫글자는 E라고 생각하고 Ea5yR3versing을 입력해보았는데 정답처리가 되었다.