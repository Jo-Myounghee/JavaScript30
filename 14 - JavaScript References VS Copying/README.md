# 1. copy 

```javascript
let age = 100;
let age2 = age;
console.log(age, age2) // 100 100
age2 = 200;
console.log(age, age2) // 100 200
```



```javascript
const players = ['Wes', 'Sarah', 'Ryan', 'Poppy'];
const team = players;
console.log(players, team)
// players = ['Wes', 'Sarah', 'Ryan', 'Poppy']
// team = ['Wes', 'Sarah', 'Ryan', 'Poppy']
team[3] = 'Lux';
// players = ['Wes', 'Sarah', 'Ryan', 'Lux']
// team = ['Wes', 'Sarah', 'Ryan', 'Lux']
```



```javascript
const players = ['Wes', 'Sarah', 'Ryan', 'Poppy'];
const team2 = players.slice;
console.log(players, team)
// players = ['Wes', 'Sarah', 'Ryan', 'Poppy']
// team = ['Wes', 'Sarah', 'Ryan', 'Poppy']
team[3] = 'Lux';
// players = ['Wes', 'Sarah', 'Ryan', 'Poppy']
// team = ['Wes', 'Sarah', 'Ryan', 'Lux']
```



```javascript
const players = ['Wes', 'Sarah', 'Ryan', 'Poppy'];
const team3 = [].concat(players);
console.log(players, team)
// players = ['Wes', 'Sarah', 'Ryan', 'Poppy']
// team = ['Wes', 'Sarah', 'Ryan', 'Poppy']
team[3] = 'Lux';
// players = ['Wes', 'Sarah', 'Ryan', 'Poppy']
// team = ['Wes', 'Sarah', 'Ryan', 'Lux']
```



```javascript
const players = ['Wes', 'Sarah', 'Ryan', 'Poppy'];
const team4 = [...players];
console.log(players, team)
// players = ['Wes', 'Sarah', 'Ryan', 'Poppy']
// team = ['Wes', 'Sarah', 'Ryan', 'Poppy']
team[3] = 'Lux';
// players = ['Wes', 'Sarah', 'Ryan', 'Poppy']
// team = ['Wes', 'Sarah', 'Ryan', 'Lux']
```



```javascript
const players = ['Wes', 'Sarah', 'Ryan', 'Poppy'];
const team5 = Array.from(players);
console.log(players, team)
// players = ['Wes', 'Sarah', 'Ryan', 'Poppy']
// team = ['Wes', 'Sarah', 'Ryan', 'Poppy']
team[3] = 'Lux';
// players = ['Wes', 'Sarah', 'Ryan', 'Poppy']
// team = ['Wes', 'Sarah', 'Ryan', 'Lux']
```



```javascript
const person = {
    name: 'Wes Bos',
    age: 80;
};

const captain = person;
captain.number = 99;
// person = {name: "Wes Bos", age: 80, number: 99}
// captain = {name: "Wes Bos", age: 80, number: 99}
```



```javascript
const person = {
    name: 'Wes Bos',
    age: 80;
};

const cap2 = Object.assign({}, person, { number: 99, age: 12 });
console.log(cap2);
// person = {name: "Wes Bos", age: 80}
// cap2 = {name: "Wes Bos", age: 12, number: 99}
```



```javascript
const wes = {
    name: 'Wes',
    age: 100,
    social:{
        twitter: '@wesbos',
        facebook: 'wesbos.developer'
    }
}

const dev = Object.assign({}, wes);

dev.social.twitter = '@coolman';

console.log(dev.social) // {twitter: "@coolman", facebook: "wesbos.ddeveloper"}
console.log(wes.social) // {twitter: "@coolman", facebook: "wesbos.ddeveloper"}
```



```javascript
const wes = {
    name: 'Wes',
    age: 100,
    social:{
        twitter: '@wesbos',
        facebook: 'wesbos.developer'
    }
}

const dev2 = JSON.parse(JSON.stringify(wes));

dev2.social.twitter = '@coolman';

console.log(wes.social) // {twitter: "@wesbos", facebook: "wesbos.ddeveloper"}
console.log(dev2.social) // {twitter: "@coolman", facebook: "wesbos.ddeveloper"}
```

