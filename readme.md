# neuron based in javascript

[![neuron-fiber on NPM](https://img.shields.io/npm/v/neuron-fiber.svg?style=flat-square)](https://www.npmjs.com/package/neuron-fiber)
[![Build Status](https://secure.travis-ci.org/rainlst/neuron-fiber.png?branch=master)](http://secure.travis-ci.org/rainlst/neuron-fiber)

> "You want to explore a forest ,then a tree is a best place to do" - stone

## Getting Started

Follow these steps:

1. [Install](#install)
2. [Usage](#usage)
3. [API](#API)
4. [Algorithm](#algorithm)
5. **[Review Example Code](https://github.com/rainlst/neuron-fiber/tree/master/example)**

## Install

```
$ npm install neuron-fiber --save
```

## Usage

```js
const { NeuronNet, NeuronLayer } = require('neuron-fiber')

/**
 *  Imagine looks like number: 0
 */
const number0 = '*****' 
              + '*   *'
              + '*   *'
              + '*****' 

/**
 *  Imagine looks like number: 1
 */
const number1 = '*    ' 
              + '*    '
              + '*    '
              + '*    '

/**
 *  Imagine looks like number: 2
 */
const number2 = '*****' 
              + '  ** '
              + ' **  '
              + '*****' 


function stringToArray(string){
  return string.replace(/\*/g,1).replace(/\s/g,0).split('')
}

const inputs = [stringToArray(number0), 
               stringToArray(number1), 
               stringToArray(number2)]


const outputs = [[0,0],
                 [0,1],  
                 [1,1]]  


function resultMap(result){
  const n = JSON.stringify(result[0].map(item=>{
    return Math.round(item)
  }))
  switch(n){
    case '[0,0]': // [0,0] >>> number: 0
      return 0
    case '[0,1]': // [0,1] >>> number: 1
      return 1
    case '[1,1]': // [1,1] >>> number: 2
      return 2
    default:
      return null
  }
}

const neuronNet = new NeuronNet(inputs, outputs, 10000)

neuronNet
  .link(new NeuronLayer(5))
  .link(new NeuronLayer(3))
  .link(new NeuronLayer(2))

neuronNet.train()

const data = '*****' 
           + '**  *'
           + '*   *'
           + '*****' 


const result = neuronNet.predict([stringToArray(data)])
console.log('result:'+resultMap(result))  //0


```
## API


### new NeuronNet(inputs, outputs, iteration)
* `inputs`:the data sample of inputs
* `outputs`:the data sample of outputs
* `iteration`:the number of training times


#### .link(options)

The options is a object obtain a layer of neural layer


#### .train()

Begin to train and modify the weight of each neural layer


#### .predict(input)

this will return results
* `input`:the data should to be predicted



### new NeuronLayer(neuronNumber)

* `neuronNumber`:the amount of neurons in this neural layer



## Algorithm
* Define variable  n(Learning rate)  which is produced by deriv sigmoid
* Define variable  Y(result) generated by sigmoid ( 0 or 1)
* Weight update : W(j) = W(j) + delta W(j)
* Delata W(j)= X(j) .* (Y-Y') * n

## License

[MIT](https://opensource.org/licenses/MIT). © 2017 lau stone

