Immutable state and merging
===========================

Like with React's `useState`, we need to update state immutably.

Here's a typical example:

    import { create } from 'zustand'
    
    const useCountStore = create((set) => ({
      count: 0,
      inc: () => set((state) => ({ count: state.count + 1 })),
    }))
    

The `set` function is to update state in the store. Because the state is immutable, it should have been like this:

    set((state) => ({ ...state, count: state.count + 1 }))
    

However, as this is a common pattern, `set` actually merges state, and we can skip the `...state` part:

    set((state) => ({ count: state.count + 1 }))
    

[

Nested objects
--------------

](#nested-objects)

The `set` function merges state at only one level. If you have a nested object, you need to merge them explicitly. You will use the spread operator pattern like so:

    import { create } from 'zustand'
    
    const useCountStore = create((set) => ({
      nested: { count: 0 },
      inc: () =>
        set((state) => ({
          nested: { ...state.nested, count: state.nested.count + 1 },
        })),
    }))
    

For complex use cases, consider using some libraries that help with immutable updates. You can refer to [Updating nested state object values](./updating-state#deeply-nested-object).

[

Replace flag
------------

](#replace-flag)

To disable the merging behavior, you can specify a `replace` boolean value for `set` like so:

    set((state) => newState, true)
    

[Edit this page](https://github.com/pmndrs/zustand/edit/main/docs/guides/immutable-state-and-merging.md)

Previous

[Updating state](/guides/updating-state)

Next

[Flux inspired practice](/guides/flux-inspired-practice)