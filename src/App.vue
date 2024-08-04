<script setup>
import { ref } from 'vue'

const hours = ref([0, 0, 0, 0, 0]);
const minutes = ref([0, 0, 0, 0, 0]);
const pricePerHour = ref(0);
const totalCost = ref(0);

// Reactive references for result
const resultHours = ref(0);
const resultMinutes = ref(0);

// Function to calculate the total time
function calculateTotalTime() {
  // Convert all times to minutes and sum them
  let totalMinutes = hours.value.reduce((acc, h, i) => {
    return acc + (h * 60 + minutes.value[i]);
  }, 0);

  // Convert total minutes back to hours and minutes
  resultHours.value = Math.floor(totalMinutes / 60);
  resultMinutes.value = totalMinutes % 60;

  totalCost.value = (totalMinutes / 60) * pricePerHour.value;
}

</script>

<template>
    <h2 style="text-align: center;">محاسبۀ ساعت کاری</h2>
    <div style="direction: rtl;" class="center">

      <!-- Header labels for hours and minutes -->
      <div class="header-row" style="direction: ltr!important;">
        <span style="width: 60px; margin: 0 5px;">ساعت</span>
        <span style="width: 60px; margin: 0 5px;">دقیقه</span>
      </div>

      <!-- Input fields for hours and minutes and price per hour -->
      <div style="direction: ltr!important;">
        <div v-for="n in 5" :key="n">
          <div class="input-row">
            <input type="number" placeholder="ساعت" v-model.number="hours[n - 1]" />
            <input type="number" placeholder="دقیقه" v-model.number="minutes[n - 1]" />
          </div>
          <div v-if="n < 5" class="plus-row">+</div>
        </div>
      </div>

      <div class="input-row">
        <label for="pricePerHour" style="margin-right: 10px;">دستمزد ساعتی:</label>
        <input type="number" id="pricePerHour" v-model.number="pricePerHour" style="width: 100px;" placeholder="قیمت" />
      </div>

      <!-- Button to trigger the calculation -->
      <button @click="calculateTotalTime">
        <h3>محاسبه</h3>
      </button>

      <!-- Display the result -->
      <h2>{{ resultHours }} ساعت و {{ resultMinutes }} دقیقه</h2>
      <h2>دستمزد کل: {{ totalCost.toLocaleString() }} تومان</h2>
    </div>
</template>

<style>
 @import url('https://cdn.jsdelivr.net/gh/rastikerdar/vazirmatn@v33.003/Vazirmatn-font-face.css');
* {
    font-family: Vazirmatn, sans-serif;
}
body {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
}
.container {
    width: 90%;
    max-width: 500px;
    margin: auto;
    text-align: center;
    }
.input-row {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 10px;
}
.plus-row {
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 17px;
      margin-bottom: 10px;
    }
input {
    width: 60px;
    margin: 0 5px;
    padding: 5px;
    text-align: center;
}
button {
    margin-top: 15px;
    width:90%;
    cursor: pointer;
}
.header-row {
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    margin-bottom: 10px;
    }
.center {
  margin: auto;
  text-align: center;
}
</style>
