# Flex Panels Image Gallery
## 구현전
- div css = display:flex
- 공간 배분
- 클릭하면 숨어있던 글자 나타나기
- 클래스 toggle
## 구현
- css 설정
```css
.panel{
    display:flex;
    justify-content:center;
    align-items:center;
    flex-direnction:colunm;
}

/*flex Items*/
.panel>*{
    flex: 1 0 auto;
    display:flex;
    justify-content:center;
    align-items:center;
}

.panel > *:first-child{
    transform:translateY(-100%)
}
.panel.open-active > *:first-child{
    transform:translateY(0)
}
.panel > *:last-child{
    transform:translateY(100%)
}
.panel.open-active > *:last-child{
    transform:translateY(0)
}
.panel.open{
    flex:5;/*패널사이즈를 키워줌 1->5로 */
    font-size:40px;
}
```
- 이벤트 생성
```js
const panels = document.querySelectorAll('.panel');

    function toggleOpen() {
        console.log('hello');
        this.classList.toggle('open');
    }

    panels.forEach(panel => panel.addEventListener('click',toggleOpen));

    function toggleActive(e) {
        //this.classList.toggle('opend-active');
        console.log(e.propertyName);
        if (e.propertyName.includes('flex')) {
            this.classList.toggle('open-active');
        }
    }

    panels.forEach(panel => panel.addEventListener('transitioned',toggleActive));
```