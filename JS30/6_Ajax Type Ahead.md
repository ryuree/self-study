# Ajax Type Ahead
## 구현전
- 검색한 내용 데이터에서 매치 시키기
- 도시, 인구 데이터 세팅
- 데이터 필터링
- 
## 구현
```js
const endpoint = 'https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json';

//도시 카운트, 빈배열
const cities = []

//호출하기
//fetch로 가져오면, 데이터 내용을 반환하지않고, 안에 약속..(?)을 반환
//fecth(endpoint).then(blob=>console.log(blob));
fecth(endpoint)
    .then(blob=>blob.json())
    .then(data => cities.push(...data));//array를 시티에 넣어줌

function findMatches(wordToMatch, cities) {
  return cities.filter(place => {
    //도시, 주 검색해서 매치할때
    const regex = new RegExp(wordToMatch, 'gi');
    return place.city.match(regex) || place.state.match(regex)
  });
}
function numberWithCommas(x) {
  return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');//정규식변환
}
function displayMatches() {
  const matchArray = findMatches(this.value, cities);
  const html = matchArray.map(place => {
    const regex = new RegExp(this.value, 'gi'); 
    const cityName = place.city.replace(regex, `<span class="hl">${this.value}</span>`);
    const stateName = place.state.replace(regex, `<span class="hl">${this.value}</span>`);
    return `
      <li>
        <span class="name">${cityName}, ${stateName}</span>
        <span class="population">${numberWithCommas(place.population)}</span>
      </li>
    `;
  }).join('');
  suggestions.innerHTML = html;
}
const searchInput = document.querySelector('.search');
const suggestions = document.querySelector('.suggestions');
searchInput.addEventListener('change', displayMatches);
searchInput.addEventListener('keyup', displayMatches);

```