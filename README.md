# joi4express [![pipeline status](https://gitlab.com/xsellier/joi4express/badges/master/pipeline.svg)](https://gitlab.com/xsellier/joi4express/commits/master)

Joiexpress validator

## Usage

```js
const express = require('express')
const app = express()
const joi4express = require('joi4express')
const helloWorld = {
  handler: (req, res) => {
    res.send('Hello-world !')
  },
  validate: {
    query: Joi.object({
      param1: Joi.string()
    }),
    params: Joi.object({
      param1: Joi.string()
    }),
    body: {
      param1: Joi.array().items({
        param2: Joi.string()
      })
    },
    headers: Joi.object({
      param1: Joi.string()
    }),
  },
  response: {
    schema: Joi.object({
      param1: Joi.string()
    }),
    status: {
      204: Joi.object({
        param2: Joi.string()
      }),
      404: Joi.object({
        error: 'Failure'
      })
    }
  }
}

app.get('/', joi4express(helloWorld))

app.listen(port, function () {
  console.log(`Example app listening on port ${port} !`)
})
```

The library also accepts Joi Options, and a Custom Joi Error Formatting option (a string).

In the following example, double quotes will be removed due to the custom error formatting expression.

```js
const removeDoubleQuotesFormatter = 'replace(/"/g, "")'
const joiOptions = null // Or some desired options
app.get('/', joi4express(helloWorld, joiOptions, removeDoubleQuotesFormatter))
```

The eval() command is run against the formatter string in the following way:

```js
message = eval(`err.message.${formatter}`)
details[].message = eval(`details[].message.${formatter}`) // for each message in the array of details.
````

## Installation

### Installing joi4express
```
  npm install joi4express --save
```

## Run Tests
Tests are written with mocha/chai.

``` bash
  $ npm test
```
