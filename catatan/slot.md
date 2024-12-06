# Slot

Basic Slot dalam Vue.js adalah fitur yang memungkinkan Anda untuk menyisipkan konten ke dalam komponen dari luar komponen tersebut.

jadi basic slot atau slot itu sendiri adalah content yang disisipkan atau ditambahkan ke dalam custom component.

# Contoh Slot

```html
<button>Register</button>

<template>
  <button>
    <slot></slot>
  </button>
</template>
```

# Implementasi

Jadi, saya akan gunakan slot pada component button

```html
<template>
  <button
    class="px-3 py-1 text-sm font-medium border border-gray-200 rounded-full :hover:bg-gray-100"
    @click="$emit('click')"
  >
    <slot></slot>
  </button>
</template>
```

lalu pada component event card, yang dimana dia memanggil component juga perlu kita ubah, sehingga seperti ini :

```html
<section class="flex justify-end p-4">
  <RoundButton @click="$emit('register')"> Register </RoundButton>
</section>
```

# Penjelasan

Kenapa kita menggunakan `slot` karena kalau kita menggunakan props untuk mengisi konten pada custom komponen kita, itu akan terbatas, jadi jika kita ingin mengirimkan lebih dari satu konten, maka kita harus menggunakan `slot`

# Penggunaan Slot

1. Fleksibilitas Konten
   Slot memungkinkan Anda untuk menyisipkan konten yang lebih kompleks dan bervariasi ke dalam komponen. Dengan menggunakan slot, Anda tidak hanya terbatas pada teks sederhana, tetapi juga dapat menyisipkan elemen HTML lainnya, seperti ikon, gambar, atau bahkan komponen lain.

<RoundButton @click="$emit('register')">
<span class="icon">🔔</span> Register
</RoundButton>

2. Keterbacaan dan Pemeliharaan Kode
   Menggunakan slot membuat kode lebih mudah dibaca dan dipahami. Ketika Anda melihat penggunaan slot, Anda langsung tahu bahwa konten yang dimasukkan ke dalam komponen dapat bervariasi. Ini membuat komponen lebih intuitif dan lebih mudah untuk dipelihara.

<RoundButton @click="$emit('register')">Register</RoundButton>

Dibandingkan dengan:

<RoundButton :title="'Register'" @click="$emit('register')"></RoundButton>

3. Reusabilitas Komponen
   Dengan slot, Anda dapat membuat komponen yang lebih generik dan dapat digunakan kembali di berbagai konteks. Anda dapat menggunakan komponen yang sama untuk berbagai jenis tombol dengan konten yang berbeda tanpa perlu membuat banyak props.

<RoundButton @click="$emit('register')">Register</RoundButton>
<RoundButton @click="$emit('cancel')">Cancel</RoundButton>

4. Pengurangan Prop Drilling
   Ketika Anda menggunakan props, Anda mungkin perlu mengoper props dari komponen induk ke komponen anak, yang dapat menyebabkan "prop drilling" (proses mengoper props melalui beberapa lapisan komponen). Dengan slot, Anda dapat langsung menyisipkan konten ke dalam komponen tanpa perlu mengoper props melalui banyak lapisan.

5. Kemudahan dalam Styling dan Penataan
   Dengan slot, Anda dapat dengan mudah menambahkan styling atau elemen tambahan di sekitar konten yang disisipkan. Ini memberikan lebih banyak kontrol atas bagaimana konten ditampilkan dan diatur.

<RoundButton @click="$emit('register')">
<span class="icon">🔔</span>
<span class="text">Register</span>
</RoundButton>
