# Use useCallback To Prevent Function Recreations

Whenever a functional React component is rerendered, it will recreate all normal functions in the component. React provided a useCallback hook that can be used to avoid that. useCallback will keep the old instance of the function between renders as long as its dependencies doesn't change.

```
import { useCallback } from 'react'

const Component = () => {
  const [value, setValue] = useState(false)

  // This function will be recreated on each render.
  const handleClick = () => {
    setValue(true)
  }

  return <button onClick={handleClick}>Click me</button>
}
```
```
import { useCallback } from 'react'

const Component = () => {
  const [value, setValue] = useState(false)

  // This function will only be recreated when the variable value updates.
  const handleClick = useCallback(() => {
    setValue(true)
  }, [value])

  return <button onClick={handleClick}>Click me</button>
}
```

This time, I won't say do this or do that. Some people would tell you to optimize each function with a useCallback hook, but I won't. For small functions like the one in the example, I can't assure it really is better to wrap the function in useCallback.

Under the hood, React will have to check dependencies on every render to know if a new function needs to be created or not, and sometimes the dependencies changes frequently anyways. The optmization useCallback gives might therefore not always be needed.

If the dependencies to the function doesn't update a lot though, useCallback can be a good optimization to avoid recreating the function on each render.
