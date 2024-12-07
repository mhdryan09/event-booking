# Named Slot

## Defining a named slot

```vue
<slot name="header"></slot>
```

## passing content to slots

```vue
<template v-slot:header></template>
```

atau bisa juga dengan cara seperti ini

```vue
<template #header></template>
```

## Usage

```html
<Component>
  <template #header> This will be rendered in the header slot </template>
</Component>
```
