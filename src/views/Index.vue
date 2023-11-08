<script setup>
import {ref} from "vue";

const pera = "Mujib, the son of a middle-class landowner, studied law and political science at the Universities of Calcutta and Dacca (now Dhaka). Although jailed briefly as a teenager for agitating for Indian independence, he began his formal political career in 1949 as a cofounder of the Awami League. The league advocated political autonomy for East Pakistan, the detached eastern part of Pakistan. Mujib’s arrest in the late 1960s incited mob violence that eroded the Pakistani president’s authority in East Pakistan."
const arrayPera = pera.split(' ');
const user_input_number = ref(0);
const user_input = ref('');
const matched = ref(0);
const not_matched = ref(0);
const time = ref(5);
const count_down_start = ref(false);
const intervalId = ref(null);

function checkWord() {
  if (user_input.value.trim().length > 0) {
    if (user_input.value.trim() === arrayPera[user_input_number.value].trim()) {
      console.log('matched');
      matched.value += 1;
    } else {
      not_matched.value += 1;
      console.log('not matched');
    }

    user_input_number.value += 1;
    user_input.value = ''
  }
}

function startCountDownIfNotStart() {
  if (!count_down_start.value) {
    count_down_start.value = true;
    intervalId.value = setInterval(() => {
      if (time.value > 0) {
        time.value--;
      } else {
        user_input.value = '';
        clearInterval(intervalId);
      }
    }, 1000);
  }
}

function restart(){
  time.value = 60;
  count_down_start.value = false;
  this.input.removeAttribute('readonly');
}

</script>

<template>
  <title>Finger Booster</title>

  <div class="h-screen flex items-center justify-center bg-gray-400">
    <div
        class="w-2/5 p-8 bg-white rounded-xl shadow-2xl h-full"
    >
      <h3 class="text-center text-2xl mb-2 bg-green-500 rounded-full p-2 text-white">
        Finger Booster
      </h3>

      <label
          for="message"
          class="block mb-2 text-sm font-medium text-gray-900">Your message</label>
      <div
          id="message"
          class="block p-2.5 w-full h-48 text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500"
      >

        <span v-for="(pera, index) in arrayPera" :key="index"
              :class="index === user_input_number ? 'bg-gray-300 text-black rounded-md' : ''">
          {{ pera }}{{ index < arrayPera.length - 1 ? ' ' : '' }}
          </span>

      </div>

      <div class="flex flex-row my-6">
        <div class="basis-2/4 m-1">
          <label
              for="large-input"
              class="block mb-2 text-sm font-medium text-gray-900">Start Typing</label>
          <input
              type="text"
              class="block w-full p-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500"
              @keydown="startCountDownIfNotStart"
              @keyup.space="checkWord"
              v-model="user_input"
              :readonly="time === 0"
          />
        </div>

        <div class="basis-1/4 m-1">
          <label
              for="large-input"
              class="block mb-2 text-sm font-medium text-white bg-green-500 rounded text-center">Time</label>
          <input
              type="text"
              class="block w-full p-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500"
              :value="time"
              readonly
          />
        </div>

        <div class="basis-1/4">
          <label
              for="large-input"
              class="block mb-2 text-sm font-medium text-white bg-green-500 rounded text-center"></label>
          <button class="w-full h-10 mt-8 text-white bg-green-500 rounded" @click="restart">
            Restart
          </button>
        </div>
      </div>


      <div class="flex flex-row p-2">
        <div class="basis-2/4 m-1">
          <label
              for="large-input"
              class="block mb-2 text-sm font-medium text-white bg-green-500 rounded text-center">Matched</label>
          <input
              type="text"
              class="block w-full p-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500"
              :value="matched"
              readonly
          />
        </div>

        <div class="basis-2/4 m-1">
          <label
              for="large-input"
              class="block mb-2 text-sm font-medium text-white bg-rose-500 rounded text-center">Not Matched</label>
          <input
              type="text"
              class="block w-full p-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500"
              :value="not_matched"
              readonly
          />
        </div>
      </div>
    </div>
  </div>
</template>
