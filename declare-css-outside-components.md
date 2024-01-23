# Declare CSS Outside Components

If you are using a CSS in JS solution, avoid declaring CSS within components.

```
import makeCss from 'some/css/in/js/library'

const Component = () => {
  // Don't do this.
  return <div className={makeCss({ background: red, width: 100% })} />
}
```

The reason why not to do it is because the object has to be recreated on every render. Instead, lift it out of the component.

```
import cssLibrary from 'some/css/in/js/library'

// Do this instead.
const someCssClass = makeCss({
  background: red,
  width: 100%
})

const Component = () => {
  return <div className={someCssClass} />
}
```
