# Use useCallback To Prevent useEffect Triggers

The previous example showed how to optimize renders with help of useCallback, in the same way, it is also possible to avoid unnecessary useEffect triggers.

```
import { useCallback, useEffect } from 'react'

const Component = ({ someProp }) => {
  // Reference to onTrigger function will only change when someProp does.
  const onTrigger = useCallback(() => {
    // Some code...
  }, [someProp])

  // useEffect will only run when onTrigger function updates.
  // If onTrigger wasn't wrapped in a useCallback, useEffect would run every time this function renders.
  useEffect(() => {
    // Some code...
  }, [onTrigger])

  return <button onClick={onTrigger}>Click me</button>
}
```
