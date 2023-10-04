# FreeCodeCamp JavaScript Algorithms and Data Structures ( Intermediate Algorithm Scripting Solutions ).
## 1-Sum All Numbers in a Range
```
function sumAll(arr) {
  arr.sort((a, b) => {
    return a - b;
  });

  let newArr = [];
  for (let i = arr[0]; i <= arr[arr.length - 1]; i++) {
    newArr.push(i);
  }

  return newArr.reduce((sum, num) => {
    return sum + num;
  }, 0);
}
```
## 2-Diff Two Arrays
```
function diffArray(arr1, arr2) {
  let newArr = arr1
    .filter((x) => !arr2.includes(x))
    .concat(arr2.filter((x) => !arr1.includes(x)));

  return newArr;
}
```
## 3-Seek and Destroy
```
function destroyer(arr, ...args) {
  return arr.filter((item) => !args.includes(item));
}
```
## 4-Wherefore art thou
```
function whatIsInAName(collection, source) {
  return collection.filter((obj) => {
    for (let key in source) {
      if (obj[key] != source[key]) {
        return false;
      }
    }
    return true;
  });
}
```
## 5-Spinal Tap Case
```
function spinalCase(str) {
  let strArr = str.split(/(?=[A-Z])|\W|_/);
  let lowerCaseStrArr = [];
  strArr.map((word) => {
    lowerCaseStrArr.push(word.toLowerCase());
  });
  // for (let i = 0; i < strArr.length; i++) {
  //   lowerCaseStrArr.push(strArr[i].toLowerCase());
  // }
  return lowerCaseStrArr.join("-");
}
```
## 6-Pig Latin
```
function translatePigLatin(str) {
  // Create variables to be used
  var pigLatin = "";
  var regex = /[aeiou]/gi;

  // Check if the first character is a vowel
  if (str[0].match(regex)) {
    pigLatin = str + "way";
  } else if (str.match(regex) === null) {
    // Check if the string contains only consonants
    pigLatin = str + "ay";
  } else {
    // Find how many consonants before the first vowel.
    var vowelIndice = str.indexOf(str.match(regex)[0]);

    // Take the string from the first vowel to the last char
    // then add the consonants that were previously omitted and add the ending.
    pigLatin = str.substr(vowelIndice) + str.substr(0, vowelIndice) + "ay";
  }

  return pigLatin;
}
```
## 7-Search and Replace
```
function myReplace(str, before, after) {
  let pattern = /^[A-Z]/;
  let testUpperBefore = pattern.test(before);
  let testUpperAfter = pattern.test(after);

  if (testUpperAfter == false && testUpperBefore == false) {
    return str.replace(before, after);
  } else if (testUpperBefore && testUpperAfter == false) {
    let newAfter = after[0].toUpperCase() + after.slice(1);
    return str.replace(before, newAfter);
  } else if (testUpperBefore == false && testUpperAfter) {
    let newAfter = after[0].toLowerCase() + after.slice(1);
    return str.replace(before, newAfter);
  }
}
```
## 8-DNA Pairing
```
function pairElement(str) {
  let pairs = {
    A: "T",
    T: "A",
    C: "G",
    G: "C",
  };
  return str.split("").map((item) => [item, pairs[item]]);
}
```
## 9-Missing letters
```
function fearNotLetter(str) {
  const alphabet = [..."abcdefghijklmnopqrstuvwxyz"];
  let strToArr = [...str];
  let firstLetterIndex = alphabet.indexOf(strToArr[0]); // Number
  let lastLetterIndex = alphabet.indexOf(strToArr[strToArr.length - 1]); // Number
  let completeStrArr = alphabet.slice(firstLetterIndex, lastLetterIndex + 1); // String

  let difference = completeStrArr
    .filter((x) => !strToArr.includes(x))
    .concat(strToArr.filter((x) => !completeStrArr.includes(x)));
  return difference[0];
}
```
## 10-Sorted Union
```
function uniteUnique(...arr) {
  let allInOne = [...arr].flat(); // [...arr]
  let noRepeat = allInOne.filter(
    (item, index) => allInOne.indexOf(item) === index
  );

  return noRepeat;
}
```
## 11-Convert HTML Entities
```
function convertHTML(str) {
  let htmlEntities = {
    "<": "&lt;",
    ">": "&gt;",
    "&": "&amp;",
    '"': "&quot;",
    "'": "&apos;",
  };
  let strArr = str.split("");
  let pattern = /[<>&"']/g;
  let strHtmlEntities = str.match(pattern);
  let sharedIndexes = [];

  if (pattern.test(str)) {
    strArr.forEach((element, index) => {
      if (strHtmlEntities.indexOf(element) !== -1) {
        sharedIndexes.push(index);
      }
    });

    sharedIndexes.forEach((index) => {
      strArr[index] = htmlEntities[strArr[index]];
    });

    return strArr.join("");
  } else {
    return str;
  }
}
```
## 12-Sum All Odd Fibonacci Numbers
```
function sumFibs(num) {
  let previousNum = 0;
  let currentNum = 1;
  let sum = 0;

  while (currentNum <= num) {
    if (currentNum % 2 !== 0) {
      sum += currentNum;
      // console.log(sum);
    }
    currentNum += previousNum;
    // console.log(currentNum);
    previousNum = currentNum - previousNum;
    // console.log(previousNum);
  }
  return sum;
}
```
## 13-Sum All Primes
```
function sumPrimes(num) {
  let arr = Array.from({ length: num - 1 }).map((x, i) => i + 2),
    sqroot = Math.floor(Math.sqrt(num)),
    numsTillSqroot = Array.from({ length: sqroot - 1 }).map((x, i) => i + 2);
  numsTillSqroot.forEach(
    (x) => (arr = arr.filter((y) => y % x !== 0 || y === x))
  );
  return arr.reduce((sum, num) => (sum += num));
}
```
## 14-Smallest Common Multiple
```
function smallestCommons(arr) {
  const min = Math.min(...arr);
  const max = Math.max(...arr);
  let scm = max;
  while (true) {
    let isScm = true;
    for (let i = min; i <= max; i++) {
      if (scm % i !== 0) {
        isScm = false;
        break;
      }
    }
    if (isScm) {
      return scm;
    }
    scm++;
  }
}
```
## 15-Drop it
```
function dropElements(arr, func) {
  while (arr.length > 0 && !func(arr[0])) {
    arr.shift();
  }
  return arr;
}

dropElements([1, 2, 3], function (n) {
  return n < 3;
});
```
## 16-Steamroller
```
function steamrollArray(arr) {
  const flat = [].concat(...arr);
  return flat.some(Array.isArray) ? steamrollArray(flat) : flat;
}
```
## 17-Binary Agents
```
function binaryAgent(str) {
  return str
    .split(" ")
    .map((b) => String.fromCharCode(parseInt(b, 2)))
    .join("");
}
```
## 18-Everything Be True
```
function truthCheck(collection, pre) {
  return collection.every(function (element) {
    return element.hasOwnProperty(pre) && Boolean(element[pre]);
  });
}
```
## 19-Arguments Optional
```
function addTogether() {
  const [first, second] = arguments;

  if (typeof first === "number") {
    if (typeof second === "number") return first + second;
    if (arguments.length === 1) return (second) => addTogether(first, second);
  }
}
```
## 20-Make a Person
```
const Person = function (first, last) {
  let firstName = first;
  let lastName = last;

  this.getFirstName = () => {
    return firstName;
  };

  this.getLastName = () => {
    return lastName;
  };

  this.getFullName = () => {
    return this.getFirstName() + " " + this.getLastName();
  };

  this.setFirstName = function (first) {
    return (firstName = first);
  };

  this.setLastName = function (last) {
    return (lastName = last);
  };

  this.setFullName = function (first, last) {
    this.setFirstName(first);
    this.setLastName(last);
    return this.getFullName();
  };
};
```
## 21-Map the Debris
```
function orbitalPeriod(arr) {
  const GM = 398600.4418;
  const earthRadius = 6367.4447;
  const a = 2 * Math.PI;
  const newArr = [];

  const getOrbPeriod = function (obj) {
    const c = Math.pow(earthRadius + obj.avgAlt, 3);
    const b = Math.sqrt(c / GM);
    const orbPeriod = Math.round(a * b);
    // create new object
    return { name: obj.name, orbitalPeriod: orbPeriod };
  };

  for (let elem in arr) {
    newArr.push(getOrbPeriod(arr[elem]));
  }

  return newArr;
}
```
