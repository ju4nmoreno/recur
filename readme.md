# 2-dimensional array

From an array of words, search an ArrayMatrix, if these words can be found
- can't find 'SOS' because the matrix only has one S
```javascript
const dic = [
  ["C", "A", "T"], 
  ["O", "S", "K"],
  ["P", "Y", "U"]
];
// Esta es la primera estructura de datos Dictionary
// La primera parte del algo es crear una funcion que dado un dictionary y un string le dice si el String hace parte del Dictinary
//algo asi esto es un predicado
function  predicate(string, dictionary) {
  return dictionary.filter(value => value == string).reduce("SOS", 
  //https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce
  )
}
// Ya con esta funcion va a usar recurcion sobre list y esa es la version mas facil

function recur(list, accumulator, dic){
  //caso base
  const [head, ...tail] = arr;
  if(list.isEmpty) { return accumulator }
  else if(predicate(head, dic) ? recur(tail, acc.append(head)): recur(tail, acc))
}

const arr = [ "COPY", "CAT", "ASK", "SOS" ] // output [ 'COPY', 'CAT', 'ASK' ]

// Y aca ejecuta el programa

recur(arr, [], dic)

// eso seria el esqueleto que habria que llenar bien



```
my solution

```javascript
const matrix = [
  ["C", "A", "T"], 
  ["O", "S", "K"],
  ["P", "Y", "U"]
];

function recu(matrixArr, word, row = 0, index = 0, indexWord = 0, findLetter = 0) {
  
  if (index < matrixArr[row].length) {
    const currentLetterMatrix = matrixArr[row][index]
    const currentLetterWord = word[indexWord]
    
    if(currentLetterMatrix === currentLetterWord) {
      matrixArr[row][index] = "%"
      indexWord += 1
      findLetter += 1
     
      if (indexWord === word.length) return word
      return recu(matrixArr, word, 0, 0, indexWord, findLetter)
    }
    
    if (currentLetterMatrix === currentLetterWord && indexWord < word.length - 1) {
      indexWord = indexWord + 1
    }
    index += 1
    
    if (index === matrixArr[row].length && row < matrixArr.length - 1) {
      index = 0
      row += 1
    } 
    
    return recu(matrixArr, word, row, index, indexWord, findLetter)
  }
  return null
}

function findWords(arr) {
  const words = []
  
  for(let word of arr) {
    const newArry = matrix.map((arr) => arr.slice())
    const isFindWord = recu(newArry, word) 
    
    if(isFindWord) {
      words.push(isFindWord)
    }
  }
  return words
}

const arr = [ "COPY", "CAT", "ASK", "SOS" ]
const result =findWords(arr)
```
