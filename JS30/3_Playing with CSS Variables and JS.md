# Playing with CSS Variables and JS
## 구현준비
- control 값 인지
- document.documentElement.style.setProperty 스타일 변경
## 구현
### html
```html
<div class="controls">
  <label for="spacing">Spacing:</label>
  <input id="spacing" type="range" name="spacing" min="10" max="200" value="10" data-sizing="px" >

  <label for="blur">Blur:</label>
  <input id="blur" type="range" name="blur" min="0" max="25" value="0" data-sizing="px">

  <label for="base">Base Color</label>
  <input id="base" type="color" name="base" value="#ffc600" />
</div>

<img src="https://source.unsplash.com/7bwQXzbF6KE/800x500" />
```
### css(sass)
```css
:root {
  --base: #ffc600;
  --spacing: 10px;
  --blur: 0px;
}

img {
  padding: var(--spacing);
  background: var(--base);
  filter: blur(var(--blur));
}

.hl {
  color: var(--base);
}
```

### js
```js
const inputs = document.querySelectorAll(".controls input");

function handleUpdate() {
  const suffix = this.dataset.sizing || "";
  document.documentElement.style.setProperty(`--${this.name}`,this.value + suffix);
}

inputs.forEach(input => input.addEventListener("change", handleUpdate));
inputs.forEach(input => input.addEventListener("mousemove", handleUpdate));
```