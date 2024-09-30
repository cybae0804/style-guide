### Functions
- Prefer names that start with a verb. Functions are natuarlly "doing" something, and what it's "doing" is the important part.
- Ex. `getValueFromData`, `createValue`, `deleteItem`

### Booleans
- Prefer names that start with `is`, `has`, `should`, etc.
- Try to avoid any negations in the name such as `not`, it becomes confusing especially with any code negations. Bad Ex. `isNotDisabled`
- Ex. `isDisabled`, `hasItem`, `shouldRender`.

### Arrays
- Prefer pluralizing any items to avoid confusion with individual items.
- Ex. `items` array and `item` entry

### Key value pairs
- Prefer `[item]By[key]`. 
- Ex. `usersByUuid` 

### Shortened names
- Generally avoid shortening names unless there's a big benefit. Shortened names are more difficult to search for.
- Ex. `error` over `e`, or `event` over `evt`.

