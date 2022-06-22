# Find all sum-zero arrays from array

```javascript
const input = [3, 4, -7, 3, 1, 3, 1, -4, -2, -2];

const getSumZeroArray = (array) => {
  const sumZeroArrays = array.reduce(
    (acc, numb) => {
      const [accumulatedSum, currentIteration, zeroSumArrays] = acc;
      const sum = accumulatedSum + numb;
      const newIteration = [...currentIteration, numb];

      if (sum === 0) {
        const newZeroSumArray = [...zeroSumArrays, newIteration];

        return [sum, newIteration, newZeroSumArray];
      } else {
        return [sum, newIteration, zeroSumArrays];
      }
    },
    [
      0, // initial sum value
      [], // array of past iterations
      [] // array of zero-sum arrays
    ]
  );

  return sumZeroArrays[2];
};

const getSumZeroArrayVariants = (source, result = []) => {
  const [, ...tail] = source;

  const sumZeroArrays = getSumZeroArray(source);

  if (tail.length === 0) {
    return result;
  } else {
    return getSumZeroArrayVariants(tail, [...result, ...sumZeroArrays]);
  }
};

const result = getSumZeroArrayVariants(input);
console.log(result);
```