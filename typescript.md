Reference: https://github.com/microsoft/TypeScript/wiki/Performance

### Aliasing
- Avoid inlining complex types into the function. Create atomic aliases whenever possible for performance, reusability, and cleanliness.

### Readonly
- Generally prefer readonly'ing everything by default, and only explicilty allowing mutation when needed.
- Ref: Rust's system https://doc.rust-lang.org/beta/book/ch03-01-variables-and-mutability.html

### Type vs Interface
- Prefer interfaces over types whenever possible

### Casting
- AVOID CASTING AS MUCH AS POSSIBLE
- Casting unstabilizes the benefits we get from using Typescript. As an extreme example, imagine if all variables in a codebase is typed with `as any`.

### Discriminated Unions/Enums
- Avoid using Typescript `enum`.
- Context: https://www.youtube.com/watch?v=0fTdCSH_QEU&embeds_referring_euri=https%3A%2F%2Fwww.redditmedia.com%2F&source_ve_path=MjM4NTE
- Context: https://dev.to/ivanzm123/dont-use-enums-in-typescript-they-are-very-dangerous-57bh
- TLDR: they are not native javascript concepts that create javascript code, unlike other Typescript APIs like `interface`.
- Prefer using something like

  ```ts
    type ValuesUnion<T extends object> = T[keyof T];

    const Color = {
      Blue: 'Blue',
      Red: 'Red',
    } as const;

    type Color = ValuesUnion<typeof Color>;
  ```
