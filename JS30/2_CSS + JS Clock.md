# CSS+JS Clock 구현

## 구현준비
- 세개의 분리된 시,분,초 바늘
- 정확한 중심을 기준으로 왼쪽에서 오른쪽으로 회전
- transform-origin
- transition-timing-function --> 전환 타이밍

## 구현
1. 시계바늘
```html
<div class="clock">
    <div class="clock-face">
        <div class="hand hour-hand"></div>
        <div class="hand min-hand"></div>
        <div class="hand second-hand"></div>
    </div>
</div>
```
2. setDate 함수를 setInterval로 1초마다 실행
```js
function setDate(){
    console.log('Hi');
}
setInterval(setDate(),1000);
```

3. setDate 함수에 현재시간의 초를 구해 1초마다 실행
```js
function setDate(){
    const now = new Date(); //새로운 날짜 생성
    const seconds = now.getSeconds(); //새로운 날짜에서 초만 가져오기
    consoel.log(seconds)
}
setInterval(setDate(),1000);
```

3. 구한 초로 비율 구한 다음 초바늘 회전율 계산
```js
//셀렉터 지정
const secondHand = document.querySelector(".second-hand");
const minsHand = document.querySelector(".min-hand");
const hourHand = document.querySelector(".hour-hand");
/*
칸의 개수 == hour(12):12시간, min(60):60분,second(60):60초

(현재값/칸의개수)*360 = 전체 움직이는 회전율

90도는 왜 더함..?오프셋..? 90도..?상쇄학위..?
*/
function setDate(){
    const now = new Date();
    const seconds = now.getSeconds();
    const secondsDegrees = ((seconds / 60) * 360) + 90;
    secondHand.style.transform = `rotate(${secondsDegrees}deg)`;
}
setInterval(setDate(),1000);
```
4. 나머지 분과 시간도 계산
```js
const mins = now.getMinutes();
const minDegrees = ((mins/60)*360)+90;
minsHand.style.transform = `rotate(${minDegrees}deg)`;

const hour = now.getHours();
const hourDegrees = ((hour/12)*360)+90;
hourHand.style.transform = `rotate(${hourDegrees}deg)`;

```

## 최종코드
```js
const secondHand = document.querySelector(".second-hand");
const minsHand = document.querySelector(".min-hand");
const hourHand = document.querySelector(".hour-hand");

function setDate(){
    const now = new Date();

    const seconds = now.getSeconds();
    const secondsDegrees = ((seconds / 60) * 360) + 90;
    secondHand.style.transform = `rotate(${secondsDegrees}deg)`;

    const mins = now.getMinutes();
    const minDegrees = ((mins/60)*360)+90;
    minsHand.style.transform = `rotate(${minDegrees}deg)`;

    const hour = now.getHours();
    const hourDegrees = ((hour/12)*360)+90;
    hourHand.style.transform = `rotate(${hourDegrees}deg)`;
}

setInterval(setDate(),1000);
```