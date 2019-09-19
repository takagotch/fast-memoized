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


