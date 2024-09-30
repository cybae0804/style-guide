### Anatomy of a component

```ts
// Prefer not destructuring anything out of React, (ex. useState) to easily identify native React hooks vs custom hooks.
import React from 'react'; 
import classNames from 'classnames';
import styles from './Component.module.scss';

/*
  - Often attach optional className prop by default to allow styles to be passed in
  - Mark all props with `readonly`, to make sure that no props are modified. This also preemptively
    prevents an issue where a ReadonlyArray<T> externally isn't compatible with non readonly array.
    You may be able to use a linter to accomplish this more easily.
*/
interface Props extends WithClassName {
  readonly isDisabled?: boolean;
  readonly items: ReadonlyArray<string>;
  readonly onItemClick?: (item: string) => void;
}

/*
  - By default, memo all components. Passing any unmemo'ed JSX as props will break the memoization, but the cost is low and benefits tend to be higher.
  - Put the `Props` type next to the actual prop, instead of `React.memo<Props>`. It's closer to the actual data in question and avoids using a generic.
  - Generally, put the hooks in the order of state, derived state, callbacks, effects. Sometimes the ordering may have to be changed with the ordering of the dependencies,
    but this allows a clearer distinction between different logic throughout the component.
  - Try to provide a falsey default prop values to optional props such as `isDisabled. Often not passing in a value to an optional prop implies a falsey behavior, and providing
    a default avoids potential type coercion downstrema.
*/
export const Component = React.memo(function _Component({ className, isDisabled = false, items, onItemClick }: Props) {
  const newItems = useItems(items);  

  /*
    Explicitly assign a return type to all `React.useMemo`'s. This creates a general contract that should not be unintentionally broken.
    Avoid typing the variable like `const sortedItems: ReadonlyArray<string>` and type the return of the callback to use TypeScript's excess property checking.
  */
  const sortedItems = React.useMemo((): ReadonlyArray<string> => {
    return [...newItems].sort();
  }, [newItems]);

  /*
    For all event handlers, name the prop as `on[Event]` and the callback itself as `handle[Implementation]`. `[Event]` and `[Implementation]` is often in the form of [Noun][Verb].
    - This closely follows the naming convnetion of the default DOM elements such as a div's onclick attribute.
    - This naming scheme avoids leaking abstraction. If you think of a component and its prosp as an API, from inside the component, we don't care what the implementation of
      onClick is. All we care about is that whenever something is clicked, we're suppose to call the `onClick` callback to notify any consumers. From outside the component,
      we are passing in an expected behavior to specific event handlers. So we may be passing in a API call handler named `handleApiCall`, but maybe we could pass it into both
      `onClick` prop or the `onBlur` prop.
    - When alphabetized, this creates a nice grouping of multiple handlers relating to the same subject. Ex. handleItemClick, handleItemCreate, handleItemDelete, etc
  */
  const handleItemClick = React.useCallback(() => {
    onItemClick(sortedItems[0]);
  }, [sortedItems])

  // Short circuit using an if statement earlier whenever possible to decrease the depth of the main JSX tree. 
  if (items == null) {
    return <span />;
  }

  // Generally prefer avoiding boolean prop shorthand for consistency and explicitness of thevalue.
  return <Button className={classNames(className, styles.root)} isDisabled={true} />;
});
```
