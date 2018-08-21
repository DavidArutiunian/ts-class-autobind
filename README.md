# Method auto-bind for TypeScript

[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

Based on [class-autobind](https://github.com/kodefox/class-autobind) package.

This package provides a single function, `autobind`, for use within a constructor to bind all methods to the instance itself.

For example, this allows us to pass a method to an event handler `element.addEventListener('click', this.onClick)` and be sure the `onClick` method will always be called with the right context.

Note: This has some specific logic for React, but could be used in any project.

## Installation:

`npm install --save ts-class-autobind`

## Usage:

```typescript jsx
import { autobind } from 'ts-class-autobind';

class MyComponent extends React.Component {
  constructor() {
    super(...arguments);
    autobind(this);
  }
  render() {
    return <button onClick={this.onClick}>Click Me</button>;
  }
  onClick() {
    console.log('Button Clicked');
  }
}
```

## Advanced Usage:

If your component will possibly be subclassed (you really should not do this, but some third-party libraries like [react-css-modules](https://npmjs.com/package/react-css-modules) do so) then you will need to specify which prototype will be the source of methods that are to be automatically bound.

```typescript jsx
import { autobind } from 'ts-class-autobind';

class MyComponent extends React.Component {
  constructor() {
    super(...arguments);
    autobind(this, MyComponent.prototype); // Note the second parameter.
  }
  render() {
    /* ... */
  }
}

class MySubClassedComponent extends MyComponent {
  /* This is probably a very bad idea. */
}
```

## License

This software is [BSD Licensed](/LICENSE.md).
