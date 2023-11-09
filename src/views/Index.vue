<script setup>
import {ref} from "vue";

const pera = "Mujib, the son of a middle-class landowner, studied law and political science at the Universities of Calcutta and Dacca (now Dhaka). Although jailed briefly as a teenager for agitating for Indian independence, he began his formal political career in 1949 as a cofounder of the Awami League. The league advocated political autonomy for East Pakistan, the detached eastern part of Pakistan. Mujib’s arrest in the late 1960s incited mob violence that eroded the Pakistani president’s authority in East Pakistan."
const arrayPera = pera.split(' ');
const user_input_number = ref(0);
const user_input = ref('');
const matched = ref(0);
const not_matched = ref(0);
const time = ref(20);
const count_down_start = ref(false);
const interval_id = ref(null);
const property_readonly = ref(false);
const show_result = ref(false);


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
    interval_id.value = setInterval(() => {
      if (time.value > 0) {
        time.value--;
      } else {
        property_readonly.value = true;
        user_input.value = '';
        clearInterval(interval_id.value);
        show_result.value = true;
      }
    }, 1000);
  }
}

function restart() {
  time.value = 20;
  property_readonly.value = false;
  count_down_start.value = false;
  user_input.value = '';
  matched.value = 0;
  not_matched.value = 0;
  user_input_number.value = 0;
  show_result.value = false;
  clearInterval(interval_id.value);
}

</script>

<template>
  <title>Fingers Booster</title>

  <div class="h-screen flex items-center justify-center bg-gray-400">
    <div
        class="w-1/5 p-8 bg-white rounded-xl shadow-2xl h-full"
    >
      <h3 class="text-center text-2xl mb-2 bg-green-500 rounded-full p-2 text-white">
        Fingers Booster
      </h3>

      <label class="block mb-2 text-sm font-medium text-gray-900">Your message</label>
      <div
          class="block p-2.5 w-full h-48 text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 overflow-auto"
          style="user-select: none;">

        <span v-for="(pera, index) in arrayPera" :key="index"
              :class="index === user_input_number ? 'bg-gray-300 text-black rounded-md' : ''">
          {{ pera }}{{ index < arrayPera.length - 1 ? ' ' : '' }}
          </span>

      </div>

      <div class="flex flex-row my-6">
        <div class="basis-3/4 m-1">
          <label
              for="large-input"
              class="block mb-2 text-sm font-medium text-gray-900">Start Typing</label>
          <input
              type="text"
              class="block w-full p-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500"
              @keydown="startCountDownIfNotStart"
              @keyup.space="checkWord"
              v-model="user_input"
              :readonly="property_readonly"
              placeholder="Type here..."
          />
        </div>

        <div class="basis-1/4 m-1">
          <label
              for="large-input"
              class="block mb-2 text-sm font-medium">Time</label>
          <input
              type="text"
              class="block w-full p-4 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-md focus:ring-blue-500 focus:border-blue-500"
              :value="time"
              readonly
          />
        </div>
      </div>

      <div class="w-full flex items-center justify-end">
        <button class="w-20 h-10 text-white bg-green-500 rounded" @click="restart">
          Restart
        </button>
      </div>

      <div v-show="show_result">
        <div class="px-4 sm:px-0 flex justify-center mt-2">
          <h3 class="text-base font-semibold leading-7 text-gray-900 border-2 border-b-green-400 w-48 text-center rounded-2xl p-2 shadow-lg">
            Result
          </h3>
        </div>
        <div class="mt-4 h-80 border-2 rounded-xl p-4">
          <div class="flex items-center justify-center">
            <img class="shadow-lg ring-1 w-20 ring-inset ring-green-300 hover:bg-gray-50 rounded-xl"
                 src="../assets/typing.png" alt="weather"/>
          </div>

          <div class=" mt-10">
            <div class="flex m-4">
              <div class="w-3/4 text-sm font-medium text-gray-900">Correct words</div>
              <div class="mt-1 text-sm text-green-500 sm:col-span-2 sm:mt-0">
                {{ matched }}
              </div>
            </div>
            <hr>
            <div class="flex m-4">
              <div class="w-3/4 text-sm font-medium text-gray-900">Wrong words</div>
              <div class="mt-1 text-sm text-rose-500 sm:col-span-2 sm:mt-0">
                {{ not_matched }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
