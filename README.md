
# safely-read

<div align="center">
	
[![Build Status](https://travis-ci.com/fabmont/safelyRead.svg?branch=master)](https://travis-ci.com/fabmont/safelyRead)
[![Coverage Status](https://coveralls.io/repos/github/fabmont/safelyRead/badge.svg?branch=master)](https://coveralls.io/github/fabmont/safelyRead?branch=master)

A Javascript utility for access nested objects safely.

</div>




## Motivation
Let's imagine you're consuming data from an API and some data inside the object given from this API doesn't exist. Your front-end should crash because of that, so using safelyRead will garantee that if the property exist, you'll get it, or transform it, otherwise, will give to you a fallback result.
SafelyRead enhance the Lodash's **get** util by provinding a transform parameter that you can modify the result of the object property.

## Instalation

1. Install the last version of safe-read:

   `npm install safely-read` or `yarn add safely-read`

2. Import it into your project:

   `const safelyRead = require('safely-read');`
   
   `// or using ES6+`
   
   `import safelyRead from 'safely-read';`

## Usage
SafelyRead provides a function that accepts four parameters.
1. **required** `{Object}`: The object you want to go through;
2. **required** `{Array<String>}`: An array of paths that each position is an element of your object;
3. **required**  `{Any}`: The fallback result, if anything go wrong with the path it will return instead;
4. **optional** `{Function}`: A function that will be triggered if the path exists.

Imagine that you have declared an object:

    const user = {
	  name: 'Bruce Wayne',
	  age: 30,
	  hero: 'Batman',
	};

And for some reason you want to access the age property of the object above by using safelyRead.

    safelyRead(user, ['age'], 'Age not found.', (age) => `${age} years old`);

If  `user.age` exists, so the fourth parameter will be triggered (returning '30 years old').
NOTE: if you didn't pass the transform function and `user.age` exist, so it will return '30' to you.

What if safelyRead can't access the property I want?

    safelyRead(user, ['car'], 'This property doesn't exist.');
  
  The `user` object doesn't contain any `car` property, so safelyRead will return the third parameter (`This property doesn't exist.`).
