<script setup>
import {computed, onBeforeMount, onMounted, ref} from "vue";

const pera = "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quos, voluptatem! Molestiae voluptas, harum, eos at dolor, quod quidem modi voluptate veniam eligendi voluptates excepturi magni? Nobis totam quaerat sunt dolorem."

const user_input = ref('');

function checkWord(){
  console.log(user_input.value);
  user_input.value =''
}

onBeforeMount(()=>{
  const pera = "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quos, voluptatem! Molestiae voluptas, harum, eos at dolor, quod quidem modi voluptate veniam eligendi voluptates excepturi magni? Nobis totam quaerat sunt dolorem."

  const arrayPera = pera.split(' ');
  console.log(arrayPera[10]);
})

</script>

<template>
  <title>Finger Booster</title>
  <div class="h-screen flex items-center justify-center bg-gray-400">
    <div
        class="max-w-sm w-1/3 mx-auto p-8 bg-white rounded-xl shadow-2xl h-full"
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
      <textarea
          id="message"
          rows="4"
          class="block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500"
          readonly
      >
      {{ pera }}
      </textarea>

      <div class="mb-6">
        <label
            for="large-input"
            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
        >Large input</label>
        <input
            type="text"
            id="large-input"
            class="block w-full p-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500"
            @keyup.space="checkWord"
            v-model="user_input"
        />
      </div>

      <div class="mb-6">
        <input
            type="text"
            id="large-input"
            class="block w-full p-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500"
            readonly
            :value="user_input"
        />
      </div>
    </div>
  </div>
</template>
