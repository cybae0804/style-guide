### Functions
- Prefer names that start with a verb. Functions are natuarlly "doing" something, and what it's "doing" is the important part, followed by the subject.
- Ex. `getValueFromData`, `createValue`, `deleteItem`

### Booleans
- Prefer names that start with `is`, `has`, `should`, etc.
- Try to avoid any negations in the name such as `not`, it becomes confusing especially with any code negations. Bad Ex. `isNotDisabled`
- Ex. `isDisabled`, `hasItem`, `shouldRender`.

### Arrays
- Prefer pluralizing any items to avoid confusion with individual items.
- Ex. `items` array and `item` entry

### Sets
- Prefer appending `Set` at the end. There's an argument for just pluralizing this like an array.
- Ex. `itemSet`

### Key value pairs
- Prefer `[item]By[key]`. 
- Ex. `usersByUuid` 

### Shortened names
- Generally avoid shortening names unless there's a big benefit. Shortened names are more difficult to search for.
- Ex. `error` over `e`, or `event` over `evt`.

### Constants 
- Whenever possible, abstract static constant variables at the root level of the file to avoid clutter.
- Prefer explicitly typing the const variables, especially reference variables, to get the benefit of Typescript autocomplete.
  - Ex. `const ITEMS: ReadonlyArray<string> = ['a', 'b', 'c'];`
- Prefer attaching the unit in the variable name whenever there's a room for confusion
- Prefer using underscore to make numbers more readable.
  - Ex. `const TIMEOUT_MS = 1_000`;
