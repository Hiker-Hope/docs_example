## Styleguide

This is a collection of simple rules and agreements on which we base our code writing culture in the project.

Most of the basic ones are automatically checked and corrected by built-in linters (ESLint, Prettier, CSSComb) so they are not indicated here


## Contents
1. [Creating a new component](#creating-a-new-component)
1. [Common rules](#common-rules)


## Creating a new component
**1.1 Component structure**
```
├── Component/
│   ├── SubComponent1/
│   ├── SubComponent2/
│   ├── SubComponent3/
│   │   ├── index.tsx                - root component SubComponent3
│   │   ├── Background/              - Background component's directory
│   │   ├── Character/               - Character component's directory
│   │   │   ├── images/              - Character component's images directory 
│   │   │   ├── index.tsx            - Character component's file
│   │   │   ├── index.scss           - Character component's CSS file
│   │   │   ├── store.ts             - Character component's store file
```

📌 Components' directories are titled in **PascalCase**.
Other directories and files are titled in  **snake_case** or **kebab-case**.

📌 Each component is created in a separate directory which contains at least 2 main files:

- `index.tsx` - with the export of the component
- `index.module.scss` - with the component's styles

📌 Title of the directory === name of the components exported from `index.tsx`.

## Common rules
**2.1 Object destructuring**

Never use `object.key` in tsx, methods or events,
use destructuring instead.

>📌 **Exemption**: if you reference the keys of the object not more than 2 times

This rule applies to **any object** if it's referenced more than 2 times.

Example:
```tsx
// 👎❌
render() {
    return (
        <div className={this.props.type}>
            <span>{this.props.value}</span>
            <input type="text" value={this.props.value} />
        </div>
    );
}

// 👍✅
render() {
    const {value, type} = this.props;
    return (
        <div className={type}>
            <span>{value}</span>
            <input type="text" value={value} />
        </div>
    );
}

// 👍✅
render() {
    return (
        <span>{this.props.value}</span>
    );
}
```
**2.2 Never use `export default`**

Use only named exports wherever possible.

**2.3 Don't use objects as props when you only need several fields of it**

Is such cases use these fields as separate props.

```tsx
// 👎❌

render() {
    return (
        <ComponentWithProps {...this.props} />
    );
}

// 👍✅
render() {
    const {prop1, prop2, prop3} = this.props;
    return (
        <ComponentWithProps
            prop1={prop1}
            prop2={prop2}
            prop3={prop3}
        />
    );
}
```

**2.4 Reuse utils functions.**

📌 There are lots of useful functions in `src/utils`.

**2.6 Always set a `displayName` to anonymous components**

You should always set displayName for components wrapped in `memo()`, `observer()`, etc. for easier debugging.

You can do it several ways:

```
// 1️⃣ Use named functions

export const component = memo(function Component(props) {})


// 2️⃣ Set the displayName directly

export const Component = memo((props) => {})

Component.type.displayName = 'Component';    // пишем через .type.displayName из-за https://github.com/facebook/react/issues/18026#issue-564002984


// 3️⃣ Use export as

const Component = (props) => {}

const wrappedComponent = memo(Component);
export {wrappedComponent as Component};
```

**2.7 Naming function and variables**

- Functions that return a boolean, as well as a boolean variables, should always start with `is/has`.

  Example:
    ```ts
    const hasPremium = true;
    const isLoggedIn = false;
    
    const isFinalTaskFinished = (): boolean => {}
    ```

**2.8 Props naming**

- any callback send as a prop to a component should start with `on`.

  Example:
    ```tsx
    const handleButtonClick = () => {};
    
    <MyComponent
        isLoaded={isLoaded}
        onButtonClick={handleButtonClick} 
    />
    ```

**2.9 Common icons and SVGs**

🔆Common icons and SVGs used in different components are stored in `src/ui/icons`.
