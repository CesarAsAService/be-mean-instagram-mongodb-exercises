# MongoDB - Aula 04 - Exercício
Autor: Frankyston Lins

## **Adicionar** 2 ataques ao mesmo tempo para os seguintes pokemons: Pikachu, Squirtle, Bulbassauro e Charmander.
```javascript
var query = { $or: [ {name: "pikachu"}, {name: "squirtle"}, {name: "bulbassauro"}, {name: "charmander"} ]};
var opts = { multi: true };
var mod = { $pushAll: { moves: ['Attack 1','Attack 2']}};
db.pokemons.update(query, mod, opts);
Updated 4 existing record(s) in 16ms
WriteResult({
  "nMatched": 4,
  "nUpserted": 0,
  "nModified": 4
})
```

## **Adicionar** 1 movimento em todos os pokemons: `desvio`.##
```javascript
var query = {};
var opts = { multi: true }
var mod = { $push: { moves: "desvio"}}
db.pokemons.update(query, mod, opts)
Updated 4 existing record(s) in 7ms
WriteResult({
  "nMatched": 4,
  "nUpserted": 0,
  "nModified": 4
})
```

## **Adicionar** o pokemon `AindaNaoExisteMon` caso ele não exista com todos os dados com o valor `null` e a descrição: "Sem maiores informações".##
```javascript
var query = { name: "AindaNaoExisteMon" };
var opts = { upsert: true };
var mod = { $setOnInsert: {
    name: "AindaNaoExisteMon"
  , attack: null
  , height: null
  , defense: null
  , moves: []
  , description: "Sem maiores informações"
}};
db.pokemons.update(query, mod, opts);
Updated 1 new record(s) in 6ms
WriteResult({
  "nMatched": 0,
  "nUpserted": 1,
  "nModified": 0,
  "_id": ObjectId("564be9c6fe48e9e114ad323c")
})
```

## Pesquisar todos o pokemons que possuam o ataque `investida` e mais um que você adicionou, escolha seu pokemon favorito.##
```javascript
var query = { moves: { $in: ["investida", "choque do trovão"] }};
db.pokemons.find(query);
{
  "_id": ObjectId("789be3c5dee01819940f2bs45"),
  "name": "Pikachu",
  "description": "Rato elétrico bem fofinho",
  "type": "elétrico",
  "attack": 55,
  "height": 0.4,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio",
    "Choque do Trovão"
  ]
}
{
  "_id": ObjectId("564beedc6dd017543940f2bf16"),
  "name": "Bulbassauro",
  "description": "Chicote de trepadeira",
  "type": "grama",
  "attack": 49,
  "height": 0.4,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio"
  ]
}
{
  "_id": ObjectId("785be3c6ee01810040f2bf17"),
  "name": "Charmander",
  "description": "Esse é o cão chupando manga de fofinho",
  "type": "fogo",
  "attack": 52,
  "height": 0.6,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio"
  ]
}
{
  "_id": ObjectId("675be3c6dd01817740f2bf27"),
  "name": "Squirtle",
  "description": "Ejeta água que passarinho não bebe",
  "type": "água",
  "attack": 48,
  "height": 0.5,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio"
  ]
}
Fetched 4 record(s) in 7ms
```

## Pesquisar **todos** os pokemons que possuam os ataques que você adicionou, escolha seu pokemon favorito.##
```javascript
var query = { moves: { $in: [/desvio/i] }};
db.pokemons.find(query);
{
  "_id": ObjectId("789be3c5dee01819940f2bs45"),
  "name": "Pikachu",
  "description": "Rato elétrico bem fofinho",
  "type": "elétrico",
  "attack": 55,
  "height": 0.4,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio",
    "Choque do Trovão"
  ]
}
{
  "_id": ObjectId("564beedc6dd017543940f2bf16"),
  "name": "Bulbassauro",
  "description": "Chicote de trepadeira",
  "type": "grama",
  "attack": 49,
  "height": 0.4,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio"
  ]
}
{
  "_id": ObjectId("785be3c6ee01810040f2bf17"),
  "name": "Charmander",
  "description": "Esse é o cão chupando manga de fofinho",
  "type": "fogo",
  "attack": 52,
  "height": 0.6,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio"
  ]
}
{
  "_id": ObjectId("675be3c6dd01817740f2bf27"),
  "name": "Squirtle",
  "description": "Ejeta água que passarinho não bebe",
  "type": "água",
  "attack": 48,
  "height": 0.5,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio"
  ]
}
Fetched 4 record(s) in 2ms
```

## Pesquisar **todos** os pokemons que não são do tipo `elétrico`.##
```javascript
var query = { type: { $ne: "elétrico" }};
db.pokemons.find(query)
{
  "_id": ObjectId("564beedc6dd017543940f2bf16"),
  "name": "Bulbassauro",
  "description": "Chicote de trepadeira",
  "type": "grama",
  "attack": 49,
  "height": 0.4,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio"
  ]
}
{
  "_id": ObjectId("785be3c6ee01810040f2bf17"),
  "name": "Charmander",
  "description": "Esse é o cão chupando manga de fofinho",
  "type": "fogo",
  "attack": 52,
  "height": 0.6,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio"
  ]
}
{
  "_id": ObjectId("675be3c6dd01817740f2bf27"),
  "name": "Squirtle",
  "description": "Ejeta água que passarinho não bebe",
  "type": "água",
  "attack": 48,
  "height": 0.5,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio"
  ]
}
{
  "_id": ObjectId("564be9c6fe48e9e114ad323c"),
  "name": "AindaNaoExisteMon",
  "attack": null,
  "height": null,
  "moves": [ ],
  "description": "Sem maiores informações"
}
Fetched 4 record(s) in 4ms
```

## Pesquisar **todos** os pokemons que tenham o ataque `investida` **E** tenham a defesa **não menor ou igual** a 49.##
```javascript
var query = { $and:[ { moves: { $in: [/investida/i]} }, { defense: { $lte: 49 } } ]};
db.pokemons.find(query)
{
  "_id": ObjectId("564beedc6dd017543940f2bf16"),
  "name": "Bulbassauro",
  "description": "Chicote de trepadeira",
  "type": "grama",
  "attack": 49,
  "height": 0.4,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio"
  ],
  "defense": 49
}
{
  "_id": ObjectId("785be3c6ee01810040f2bf17"),
  "name": "Charmander",
  "description": "Esse é o cão chupando manga de fofinho",
  "type": "fogo",
  "attack": 52,
  "height": 0.6,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio"
  ],
  "defense": 43
}
{
  "_id": ObjectId("789be3c5dee01819940f2bs45"),
  "name": "Pikachu",
  "description": "Rato elétrico bem fofinho",
  "type": "elétrico",
  "attack": 55,
  "height": 0.4,
  "moves": [
    "investida",
    "esquiva",
    "jogar areia",
    "desvio",
    "Choque do Trovão"
  ],
  "defense": 40
}
Fetched 3 record(s) in 7ms
```

## Remova **todos** os pokemons do tipo água e com attack menor que 50.
```javascript
var query = { $and:[ { type: "água" }, { attack: { $lt: 50 }} ]};
db.pokemons.remove(query);
Removed 1 record(s) in 4ms
WriteResult({
  "nRemoved": 1
})
```
