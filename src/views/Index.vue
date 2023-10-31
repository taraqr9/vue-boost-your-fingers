<script setup>
import {ref} from "vue";

const pera = "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quos, voluptatem! Molestiae voluptas, harum, eos at dolor, quod quidem modi voluptate veniam eligendi voluptates excepturi magni? Nobis totam quaerat sunt dolorem."
const arrayPera = pera.split(' ');
const user_input_number = ref(0);
const user_input = ref('');

function checkWord() {
  if (user_input.value.trim() === arrayPera[user_input_number.value].trim()) {
    console.log('matched');
  } else {console.log('not matched');
  }

  user_input_number.value += 1;
  user_input.value = ''
}

</script>

<template>
  <title>Finger Booster</title>

  <div class="h-screen flex items-center justify-center bg-gray-400">
    <div
        class="max-w-sm w-full mx-auto p-8 bg-white rounded-xl shadow-2xl h-full"
    >
      <h3
          class="text-center text-2xl mb-2 bg-green-500 rounded-full p-2 text-white"
      >
        Finger Booster
      </h3>

      <label
          for="message"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
      >Your message</label
      >
      <div
          id="message"
          class="block p-2.5 w-full h-48 text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500"
      >

        <span v-for="(pera, index) in arrayPera" :key="index" :class="index === user_input_number ? 'bg-gray-300 text-black rounded-md' : ''">
          {{ pera }}{{ index < arrayPera.length - 1 ? ' ' : '' }}
          </span>

      </div>

      <div class="mb-6">
        <label
            for="large-input"
            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"></label>
        <input
            type="text"
            id="large-input"
            class="block w-full p-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500"
            @keyup.space="checkWord"
            v-model="user_input"
        />
      </div>
    </div>
  </div>
</template>
