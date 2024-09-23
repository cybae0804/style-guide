### Anatomy of a component

```ts
import React from 'react';

interface Props {
  readonly items?: ReadonlyArray<string>;
}

export const Component = React.memo(function _Component({ items }: Props) {
  const newItems = useItems(items);  

  if (items == null) {
    return <span />
  }

  return <div />
});
```
