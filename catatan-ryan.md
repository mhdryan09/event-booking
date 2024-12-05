# Props

- Component tags using PascalCase

- Props names using camelCase

```js
defineProps({
  greetingMessage: String
});
```

- Passing props using kebab-case

```html
<MyComponent :greeting-message="hello" />
```
