# 2 dimensional array

From an array of words, search an ArrayMatrix, if these words can be found
- can't find 'SOS' because the matrix only has one S
```javascript
const matrix = [
  ["C", "A", "T"], 
  ["O", "S", "K"],
  ["P", "Y", "U"]
];

const arr = [ "COPY", "CAT", "ASK", "SOS" ] // output [ 'COPY', 'CAT', 'ASK' ]
```
my soluction

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
