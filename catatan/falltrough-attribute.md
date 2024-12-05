# Fall Trough Attribute

- Attribute or `v-on` listener not explicitly defined using `defineProps` or `defineEmits`

- class and style will be merge

jadi, ketika kita menambahkan class ke dalam sebuah custom component, maka class tersebut akan ditambahkan ke dalam root element dari komponent tersebut

jadi semisal, saya ingin menambahkan text red pada button register,

```html
<EventCard
  v-for="i in 8"
  :key="i"
  title="Vue Conference 2024"
  when="April 15, 2024"
  description="Conference about Vue and JavaScript"
  @register="console.log('registered!')"
  class="text-red-500"
/>
```

nah ini yang terjadi adalah, semua text menjadi merah, padahal niat saya itu mau kasih text nya ke button register nya saja.

kemudian saya akan membuat reusable component dari button

```html
<template>
  <button
    class="px-3 py-1 text-sm font-medium border border-gray-200 rounded-full :hover:bg-gray-100"
    @click="$emit('click')"
  >
    {{ label }}
  </button>
</template>

<script setup>
  defineProps({
    label: String
  });
</script>
```

lalu saya panggil di dalam component event card

```html
<section class="flex justify-end p-4">
  <button label="Register" @click="$emit('register')" />
</section>
```

nah ada masalah yang terjadi, yaitu ketika saya klik button register, maka log registered tampil 2 kali

kenapa bisa terjadi? karena vue tidak tahu bahwa pada component button itu kita juga menjalankan event click

maka solusinya adalah, setiap kali kita memanggil atau mengirimkan sebuah event, maka kita harus menggunakan `defineEmits`

jadi cukup tambahkan `defineEmits(['click']);` pada component button
