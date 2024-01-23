#
Use useState Instead of Variables
This first one should be a basic one, but I still see developers doing this, sometimes even seniors. To store a state in React you should always use one of the React hooks, like useState or useReducer. Never declare the state directly as a variable in a component. Doing so will redeclare the variable on every render which means that React cannot memoize things it normally memoizes.

```
import AnotherComponent from 'components/AnotherComponent'

const Component = () => {
  // Don't do this.
  const value = { someKey: 'someValue' }

  return <AnotherComponent value={value} />
}
```

In the case above, AnotherComponent and everything that depends on value will rerender on every render, even if they are memoized with memo, useMemo or useCallback.

If you would add a useEffect to your component with value as a dependency, it would trigger on every render. The reason for that is that the JavaScript reference for value will be different on every render.

By using React's useState, React will keep the same reference for value all until you update it with setValue. React will then be able to detect when to and when not to trigger effects and recalculate memoizations.

```
import { useState } from 'react'
import AnotherComponent from 'components/AnotherComponent'

const Component = () => {
  // Do this instead.
  const [value, setValue] = useState({ someKey: 'someValue' })

  return <AnotherComponent value={value} />
}
```

If you only need a state that is initiated once, and then never updated, then declare the variable outside the component. When doing that, the JavaScript reference will never change.

```
// Do this if you never need to update the value.
const value = { someKey: 'someValue' }

const Component = () => {
  return <AnotherComponent value={value} />
}
```
