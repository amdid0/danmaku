# 📘 Danmaku `.tan` 가이드

## 📌 현재구현왈료



## 명령어 목록
### at time {}
```tan
at <time_ms> {
    // 이 시점에 실행될 명령들
}
```

- `at <time_ms>`: 해당 시간(밀리초)에 탄막 스폰 명령을 실행
- 블록 {  } 내부에 명령들을 나열

---
### 1. `shape("파일이름")`

탄막 모양을 설정

```tan
shape("circlebullet.png")
```

- 이후 생성되는 탄막은 이 모양을 사용
- 문자열 리터럴

---

### 2. `fireS(x, y, speed, angle)`

직선 탄막 생성 (직선운동함)

```tan
fireS(100, 200, 4.5, 270)
```

- `x`, `y`: 발사 위치
- `speed`: 픽셀/초
- `angle`: 발사 방향 (도 단위, 0 = 오른쪽, 90 = 아래)

---

### 3. `await(ms)`

시간 지연 (현재 블록 내에서)

```tan
await 500
```

- 지정한 시간(밀리초)만큼 기다리고 다음 명령 실행

---

### 4. `for문`

반복 루프

```tan
for (int i = 0; i < 5; i = i + 1) {
    float angle = i * (360 / 5)
    fireS(100, 100, 3.0, angle)
}
```
※ 현재는 변수 대입 및 표현식 연산은 제한적으로 지원 (확장 가능)

---

### 5. 함수정의선언호

##  표현식 (Expression)

- **숫자 리터럴**: `100`, `3.5`, `0.0` 등
- **수식 지원**: `i + 1`, `360 / count` 등
- **변수 사용**: `i`, `angle` (지역 변수만 가능)

---

## ex

```tan
function burst(x, y, count, speed) {
    for (int i = 0; i < count; i = i + 1) {
        float angle = i * (360 / count)
        fireS(x, y, speed, angle)
    }
}

at 0 {
    shape("circleblue.png")
    burst(200, 250, 12, 2.5)
}

at 1000 {
    shape("circlered.png")
    burst(200, 250, 18, 3.5)
}

at 2000 {
    shape("circlegreen.png")
    burst(200, 250, 36, 1.5)
}

```

---

## 향후 지원 예정

| 명령어 | 설명 |
|--------|------|
| `fireC(...)` | 곡선 탄막 생성 (구상 중) |
|탄막그루핑|한번에모앗다가빵|

막뱀탄이나 그런거요
레이저탄막이나..

---

## 원리

- `.tan` 사용
- `.dmbin`은 `.tan`을 컴파일한 바이너리 파일
----
1. `.tan`을 작성
2. `compile_tool`로 `.dmbin`으로 컴파일
3. 게임 실행 시 `.dmbin`을 읽어 탄막 재생
