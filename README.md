# 만든이유
메이플스토리 게임을 하는데, 내가 원하는 옵션을 뽑기 위해서는 `수상한 큐브`라는 아이템을 돌려서 내가 원하는 옵션이 나올 때 까지 반복해서 돌려야 했다. <br>
이 불편함을 매크로로 해결하기 위해 만들었다.

---
# 작동원리
1. 메이플스토리 화면을 모니터 상단 왼쪽에 고정시킨다. (pyautogui)
2. 메이플 인벤토리 창을 화면에 고정 시킨다. (pyautogui)
3. 큐브 각각의 옵션 3개를 이미지로 가져온다. (opencv)
4. 이미지에는 STR 3%, DEX 6%, 공격력 6% 등등의 옵션이 있는데, 이 옵션 이미지를 문자열로 바꾼다. <br> (OCR-Tesseract)
   ex) STR 3% (IMAGE) -> STR 3% (STRING)
5. 문자열을 비교해 내가 원하는 스탯이 맞는지 비교해서 맞다면 현재 아이템 큐브 돌리는것을 멈추고, 다음 아이템으로 넘어간다. (최대 128개 아이템)

---
# 프로그램 화면
![image](https://github.com/minseojo/maple-macro/assets/64322765/a2148885-52c5-4a7c-9f11-7c8d95063967)

---
# OCR 이용한 이유 
처음에는 굳이 이미지를 바꿔야해? 그냥 STR 6% 이미지 저장해놓고, 이미지끼리 비교하면 안되나? <br>
이런식으로 구현했었는데, 내가 원하는대로 작동이 안되서 OCR을 이용했다. <br>
ex) 올스탯 3%를 올스탯 3%, 올스탯 6% 두개와 비교하면 일치율이 비슷하게 나온다. <br> 
그래서 일치율이 높다고 무조건 같은 스탯이 아니었고, 이런 상황 뿐만 아니라 꽤 많은 문제가 있었다. <br>

---
# OCR 진행 중 문제
OCR을 이용한다고 해서 진행이 수월하게 된건 아니다. <br>
테서렉트가 영어 숫자는 100% 인식하는데, 한글 해석을 제대로 못했다. 아무래도 캡쳐해서 가져오는 옵션 부분의 이미지가 작아서 그런거 같다. <br>
ex) `올스탯 3%` -> 간ㅌㅋ ㅌ칸ㅌ ㅋ <br>
예를 들어 올스탯 3퍼를 해석하면 위처럼 해석된다. 그래서 내가 일일이 비교해서 일치 시켜줬다. 그래서 3개의 경우 빼고는 100% 일치한다. 3개의 경우는 내가 큐브를 몇천개 돌리면서 보지 못한 스탯이다.
- 2번째줄 올스탯 6%
- 3번째줄 올스탯 6%
- 3번째줄 공격력 6%
위 3개의 경우는 100% 확신을 못하지만 이외의 경우는 확실히 동작한다. <br>

---
# 소감
매크로를 만들면서 내가 노동했다. - OCR 진행 중 문제가 발생해 한글을 내가 직접 매칭 시켜줬기 떄문이다. ex) `if ("간ㅌㅋ ㅌ칸ㅌ ㅋ") 올스탯3%++;` <br>
좋은 데이터, 많은 데이터의 중요성을 깨달았다.

---
# 2021년 코드 => 2023년 코드 변경 후 달라진 점
2021년에 잠재능력 3줄을 이미지로 가져와 각 스탯에 맞는 이미지를 화면 상단에서부터 찾았다. 정확도가 생각보다 높지 않았다. <br>
그래서 2023년에 장재능력 3줄을 이미지로 가져온 후, 이미지를 직접 찾는게 아니라 각 이미지를 한글로 변환해서 직접 비교했다. <br>
#### 스탯 종류: STR, DEX, LUK, INT, 공격력, 마력, 올스탯 - 7개
#### 퍼센트 종류: 3%, 6% - 2개
#### 잠재능력 3줄 
따라서 42 개 중에 아래 3개의 경우를 제외하고는 모두 동작한다. 따라서 정확도는 `약 93%` 다. <br>
- 2번째줄 올스탯 6%
- 3번째줄 올스탯 6%
- 3번째줄 공격력 6%

# ⚠ 주의
바로 사용하면 적용 안됨.
테서렉트를 따로 설정해야 한다.

