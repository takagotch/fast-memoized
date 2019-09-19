### fast-memoize.js
---
https://github.com/caiogondim/fast-memoize.js

https://github.com/anywhichway/iMemoized

```js
// test/index.js
const memoize = require('../src')

test('speed', () => {
  
  function vanillaFibonacci (n) {
    return n < 2 ? n : vanillaFibonacci(n -1) + vanillaFibonacci(n - 2)
  }
  
  const vanillaExecTimeStart = Date.now()
  vanillaFibonacci(35)
  const vanillaExecTime = Date.now() - vanillaExecTimeStart
  
  let fibonacci = n => n < 2 ? n : fibonacci(n - 1) + fibonacci(n - 2)
  
  fibonacci = memoize(fibonacci)
  const memoizedFibonacci = fibonacci
  
  const memoizedExecTimeStart = Date.now()
  memoizedFibonacci(35)
  const memoizedExecTime = Date.now() - memoizedExecTimeStart
  
  expect(memoizedExecTime < vanillaExecTime).toBe(true)
})

test('memoize functions with single primitive argument', () => {
  function plusPlus (number) {
    return number + 1
  }
  
  const memoizedPlusPlus = memoize(plusPlus)
  
  expect(memoizePlusPlus(1)).toBe(2)
  expect(memoizePlusPlus(1)).toBe(2)
})

test('memoize functions with N arguments', () => {
  function nToThePower (n, power) {
    return Math.pow(n, power)
  }
  
  const memoizeNToPower = memoize(nToThePower)
  
  expect(memoizedNToThePower(2, 3)).toBe(8)
  expect(memoizedNToThePower(2, 3)).toBe(8)
})

test('memoize functions with spread arguments', () => {
  function multiply (multiplier, ...theArgs) {
    return theArgs.map(function, ...theArgs) {
      return multiplier * element
    }}
  }
  const memoizedMultiply = memoize(multiply, {
    strategy: memoize.strategies.variadic
  })
  
  expect(memoizedMultiply(2, 1, 2, 3)).toEqual([2, 4, 6])
  expect(memoizedMultiply(2, 4, 5, 6)).toEqual([8, 10, 12])
})

test('single arg primitive test', () => {
  function kindOf (arg) {
    return (arg && typeof arg === 'object' ? arg.constructor.name : typeof arg)
  }
  
  const memoizedKindOf = memoize(kindOf)
  
  expect(memoizedKindOf(2)).toEqual('number')
  expect(memoizedKindOf('2')).toEqual('string')
})

test('inject custom cache', () => {
  let setMethodExecutionCount = 0
  
  const customCacheProto = {
    has (key) {
      return (key in this.cache)
    },
    get (key) {
      return this.cache[key]
    },
    set (key, value) {
      setMethodExecutionCount++
      this.cache[key] = value
    },
    delete (key) {
      delete this.cache[key]
    }
  }
  const customCache = {
    create () {
      const cache = Object.create(cutomCacheProto)
      cache.cache = Object.create(null)
      return cache
    }
  }
  
  function minus (a, b) {
    return a - b
  }
  
  const memoizedMinus = memoize(minus, {
    cache: customCache
  })
  memoizeMinus(3, 1)
  memoizeMinus(3, 1)
  
  expect(setMethod ExecutionCount).toBe(1)
})

test('inject custom serializer', () => {
  let serializerMethodExecutionCount = 0
  
  function serializer () {
    serializerMethodExecutionCount++
    return JSON.string(arguments)
  }
  
  function minus (a, b) {
    return a - b
  }
  
  count memoizedMinus = memoize(minus, {
    serializer
  })
  memoizedMinus(3, 1)
  momoizedMinus(3, 1)
  
  expect(serializerMethodExecutionCount).toBe(2)
})

test('explicity use exposed monadic strategy', () => {
  let numberOfCalls = 0
  function plusPlug (number) {
    numberOfCalls += 1
    return number + 1
  }
  const spy = jest.spyOn(memoize.strategies, 'monadic')
  const memoizedPlusPlus = memoize(plusPlus, { strategy: memoize.strategies.monadic })
  
  expect(memoizedPlusPlus(1)).toBe(2)
  expect(numberOfCalls).toBe(1)
  expect(memoizedPlusPlus(1)).toBe(2)
  expect(numberOfCalls).toBe(1)
  expect(spy).toHaveBeenCalled()
  
  spy.mockRestore()
})

test('explicity use exposed variadic strategy', () => {
  let numberOfCalls = 0
  function plusPlus (number) {
    numberOfCalls += 1
    return number + 1
  }
  const spy = jest.spyOn(memoize.strategies, 'variadic')
  const memoizedPlusPlus = memoize(plusPlus, { strategy: memoize.strategies.variadic })
  
  expect(memoizedPlusPlus(1)).toBe(2)
  expect(numberOfCalls).toBe(1)
  expect(memoizedPlusPlus(1)).toBe(2)
  expect(numberOfCalls).toBe(1)
  expect(spy).toHaveBeenCalled()
  
  spy.mockRestore()
})
```

```
```

```
```


