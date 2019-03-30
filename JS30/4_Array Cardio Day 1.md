# Array Cardio Day 1
## Code
```js
const inventors = [
    {first : 'Albert',last:'Einstein',year:1879,passed:1955},
    {first : 'Issac',last:'Newton',year:1643,passed:1727},
    {first : 'Galileo',last:'Galilei',year:1564,passed:1642},
    {first : 'Marie',last:'Curie',year:1867,passed:1934},
    {first : 'Johannes',last:'Kepler',year:1571,passed:1630},
    {first : 'Nicolaus',last:'Copernicus',year:1473,passed:1543},
    {first : 'Max',last:'Planck',year:1858,passed:1947}
];
const people =[
    'Beck, Glenn', 'Becker, Carl', 'Beckett, Samuel',
     'Beddoes, Mick', 'Beecher, Henry', 'Beethoven, Ludwig', 'Begin, Menachem', 'Belloc, Hilaire', 
     'Bellow, Saul', 'Benchley, Robert', 'Benenson, Peter', 'Ben-Gurion, David', 'Benjamin, Walter',
      'Benn, Tony', 'Bennington, Chester', 'Benson, Leana', 'Bent, Silas', 'Bentsen, Lloyd', 
      'Berger, Ric', 'Bergman, Ingmar', 'Berio, Luciano', 'Berle, Milton', 'Berlin, Irving', 
      'Berne, Eric', 'Bernhard, Sandra', 'Berra, Yogi', 'Berry, Halle', 'Berry, Wendell', 
      'Bethea, Erin', 'Bevan, Aneurin', 'Bevel, Ken',
       'Biden, Joseph', 'Bierce, Ambrose', 'Biko, Steve', 'Billings, Josh', 'Biondo, Frank', 
       'Birrell, Augustine', 'Black, Elk', 'Blair, Robert', 'Blair, Tony', 'Blake, William'
]
```
#### 1. Array.prototype.filter()
- filter the list of inventors for those who were born in the 1500's
```js
const fifteen = inventors.filter(inventor => inventor.year >== 1500 && inventor.year < 1600)

/*const fifteen = inventors.filter(inventor => {
    if(inventor.year >== 1500 && inventor.year < 1600){
        return true; //keep it;
    }
});*/
```

#### 2. Array.prototype.map()
- Give us an array of the inventory first and last names
```js
//const fullNames = inventors.map(inventor => inventor.first+ ' ' + inventor.last);

const fullNames = inventors.map(inventor => `${inventor.first}${inventor.last}`);
```

#### 3. Array.prototype.sort()
- Sort the inventors by birthday, oldest to yongest
```js
/*const oldered = inventors.sort(function(a,b){
    if(a.year > b.year){
        return 1;
    }else{
        return -1;
    }
});*/
const oldered = inventors.sort((a,b)=>a.year > b.year? 1 : -1);

```

#### 4. Array.prototype.reduce()
- How many years did all the inventors live?
```js
/*var totalYears = 0;
for(var i=0;i<inventors.length;i++){
    totalYears += inventors[i].year
}*/

const totalYears = inventors.reduce((total,inventor)=>{
    return total + (inventor.passed - inventor.year)
},0)
```
- Sort the inventors by years lived
```js
/*const oldest = inventors.sort(function(a,b){
    const lastGuy = a.passed - a.year;
    const nextGuy = b.passed - b.year;
    if(lastGuy>nextGuy){
        return -1;
    }else{
        return 1;
    }
})*/
const oldest = inventors.sort(function(a,b){
    const lastGuy = a.passed - a.year;
    const nextGuy = b.passed - b.year;

    return lastGuy>nextGuy ? -1:1
})
```
#### Create a list of Boulevards in Paris the contain 'de' anywhere in the name
```js
// https://en.wikipedia.org/wiki/Category:Boulevards_in_Paris
const category = document.querySelector('.nw-catagory');
const links = Array.from(catagory.querySelectorAll('a'));
//const links = [...catagory.querySelectorAll('a')];

const de = link
            .map(link => link.textContent)
            .filter(streetName => streetName.includes('de'));
```
#### Sort Exercise
```js
//Sort the people alphabetically by last name
const alpha = people.sort((lastOne, nextOne) => {
        const [aLast, aFirst] = lastOne.split(', ');
        const [bLast, bFirst] = nextOne.split(', ');
        return aLast > bLast ? 1 : -1;
});
```

#### Reduce Exercise
```js
// Sum up the instance of each of these
const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car','truck'];

const transportation = data.reduce((obj, item) => {
    if (!obj[item]) {
        obj[item] = 0;
    }
    obj[item]++;
        return obj;
    }, {});
```
