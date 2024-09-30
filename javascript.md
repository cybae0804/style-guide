### `undefined` vs `null`
- Always prefer using `undefined` whenever possible.
- `undefined` and `null` are two different ways of representing an empty state in javascript, and using both can lead to confusing empty state behaviors.
- Soft comparison such as `== null` or `== undefined` will compare against either `null` or `undefined`.
- This additionally mimics the [nullish coalescing](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing) behavior.
