# Drum Kit 구현

## 구현준비
- keyboard를 눌렀을때 이벤트를 감지
- 이벤트 발생시 data-key값과 일치하는 dom의 audio 재생
- 이벤트가 발생했을때 data-key를 구분해서 css(.playing) 적용
- 이벤트가 끝나면 추가 된 클래스 제거
- data-key는 keycode.info에서 키보드와 일치하는 번호를 사용

## 구현

1. 키보드 이벤트 발생
```js
window.addEventListener('keydown',function(e){
   console.log(e);
});
```
2. keydown이벤트: 이벤트객체에 keycode 값 일치시키기
```js
window.addEventListener('keydown',function(e){
    console.log(e.keyCode); //keycode값 찾기
    const audio = document.querySeletor(`audio[data-key="${e.keyCode}"]`); //audio data-key와 keycode값 일치
    const key = document.querySeletor(`.key[data-key="${e.keyCode}"]`);//key data-key와 keycode값 일치
});
```
3. audio 이벤트
```js
window.addEventListener('keydown',function(e){
    console.log(e.keyCode);
    const audio = document.querySeletor(`audio[data-key="${e.keyCode}"]`);
    const key = document.querySeletor(`.key[data-key="${e.keyCode}"]`);
    if(!audio) return ; // audio값이 없으면 이벤트 중지, 있으면 이벤트 실행
    audio.currentTime = 0; //여러번 실행될 수 있게
    
    audio.play();
});
```
4. 누른 키보드에 keycode와 동일한 key에 클래스 추가
```js
window.addEventListener('keydown',function(e){
    const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
    if(!audio) return ; //stop the function from running all together
    audio.currentTime = 0; //rewind to the start

    audio.play();
    key.classList.add('playing'); //클래스 추가
    //key.classList.remove('playing'); //클래스 제거
    //key.classList.toggle('playing'); // 클래스 추가제거 토글
});
```
5. key클래스를 가진 모든 객체 선택
- 각 key 객체에 이벤트 감지 위해서
```js
const keys = document.querySelectorAll(".key");
```
6. key 객체에 이벤트 생성
```js
function removeTransition(){
    if(e.propertyName !== 'transform') return; //Transform 이벤트가 아니면 스킵
    this.classList.remove('playing');//클릭한 해당 키 클래스 제거
}

const keys = document.querySelectorAll(".key");
//key.addEventListner('transitionend');
key.forEach(key=>key.addEventListner('transitionend',removeTransition));
```
## 최종 코드
```js
function playAudio(e){
    const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
    if(!audio) return ; 
    audio.currentTime = 0;

    audio.play();
    key.classList.add('playing');
}
function removeTransition(){
    if(e.propertyName !== 'transform') return;
    this.classList.remove('playing');
}
const keys = document.querySelectorAll(".key");

key.forEach(key=>key.addEventListner('transitionend',removeTransition));

window.addEventListener('keydown',playAudio);
```