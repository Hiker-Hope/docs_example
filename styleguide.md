## Styleguide

Это сводка простых правил и соглашений, которые мы используем в проекте.

Большая часть из них проверяется и чинится встроенными линтерами (ESLint, Prettier, CSSComb), поэтому здесь они не описываются.


## Содержание
1. [Создание новых компонентов](#Создание-новых-компонентов)
1. [Общие правила](#Общие-правила)
1. [Описание типов](#Типы)
1. [Стили](#Стили)


## Создание новых компонентов
**1.1 Структура компонента**
```
├── Component/
│   ├── SubComponent1/
│   ├── SubComponent2/
│   ├── SubComponent3/
│   │   ├── index.tsx                - корневой компонент SubComponent3
│   │   ├── Background/              - директория компонента Background
│   │   ├── Character/               - директория компонента Character
│   │   │   ├── images/              - директория с изображениями, используемыми в компоненте Character 
│   │   │   ├── index.tsx            - файл с компонентом Character
│   │   │   ├── index.scss           - файл со стилями для компонента Character
│   │   │   ├── store.ts             - файл со стором компонента Character
```
📌 Для именования папок компонентов используется **PascalCase**.
Для остальных папок и файлов - **snake_case** или **kebab-case**.

📌 Каждый компонент создаётся в папке, которая содержит 2 основных файла:

- `index.tsx` - из него экспортируется компонент
- `index.module.scss` - основные стили (название блока подтянется из названия папки).

📌 Название директории === названию компонента, экпортируемого из `index.tsx`.

## Общие правила
**2.1 Деструктуризация объектов**

Не используйте `object.key` в tsx, в методах и событиях,
вместо этого используйте деструктуринг.

>📌 **Исключение**: если обращение к полям объекта происходит не более двух раз

Это правило касается полей **любого объекта**, если он используется более двух раз.

Пример:
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
**2.2 Не используйте `export default`**

**2.3 Не прокидывайте в пропсы компонента целый объект, если вам из него нужны только несколько полей**

В таком случае прокидывайте только конкретные необходимые поля.

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

**2.4 Переиспользуйте утилитарные функции.**

📌 В папке `src/utils` лежит много полезных утилит, которые можно и нужно переиспользовать, а не копипастить в свой компонент.


**2.6 Обязательно добавляйте `displayName` анонимным компонентам**

Всегда необходимо указывать displayName для компонентов с `memo()`, `observer()` и т.п.

Это можно сделать разными способами:

```
// 1️⃣ Использовать именованную функцию 

export const component = memo(function Component(props) {})


// 2️⃣ Напрямую прописать displayName

export const Component = memo((props) => {})

Component.type.displayName = 'Component';    // пишем через .type.displayName из-за https://github.com/facebook/react/issues/18026#issue-564002984


// 3️⃣ Ипользовать export as

const Component = (props) => {}

const wrappedComponent = memo(Component);
export {wrappedComponent as Component};
```

Все способы рабочие, можно использовать любой — главное, чтобы в React DevTools было как можно меньше `Аnonymous` компонентов.


**2.7 Именование функций и переменных**

- Функции, возвращающие boolean, и boolean-переменные всегда называем с префиксом `is/has`.

  Пример:
    ```ts
    const hasPremium = true;
    const isLoggedIn = false;
    
    const isFinalTaskFinished = (): boolean => {}
    ```

**2.8 Именование Props**

- любые коллбеки, передаваемые в компонент, всегда называем с префиксом `on`.

  Пример:
    ```tsx
    const handleButtonClick = () => {};
    
    <MyComponent
        isLoaded={isLoaded}
        onButtonClick={handleButtonClick} 
    />
    ```

**2.9 Общие иконки и svg**

🔆Общие иконки и SVG, используемые в разных компонентах, хранятся в `src/ui/icons`.
