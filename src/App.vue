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
    <div style="direction: rtl;" class="center neomorphism">

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
/* button {
    margin-top: 15px;
    width:90%;
    cursor: pointer;
} */
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

button {
  display: inline-block;
  transition: all 0.2s ease-in;
  position: relative;
  overflow: hidden;
  z-index: 1;
  color: #090909;
  padding: 0.3em 0.5em;
  cursor: pointer;
  font-size: 18px;
  border-radius: 0.5em;
  background: #e8e8e8;
  border: 1px solid #e8e8e8;
  box-shadow: 6px 6px 12px #c5c5c5, -6px -6px 12px #ffffff;
  width:90%;
  height: 2%;
}

button:active {
  color: #666;
  box-shadow: inset 4px 4px 12px #c5c5c5, inset -4px -4px 12px #ffffff;
}

button:before {
  content: "";
  position: absolute;
  left: 50%;
  transform: translateX(-50%) scaleY(1) scaleX(1.25);
  top: 100%;
  width: 140%;
  height: 180%;
  background-color: rgba(0, 0, 0, 0.05);
  border-radius: 50%;
  display: block;
  transition: all 0.5s 0.1s cubic-bezier(0.55, 0, 0.1, 1);
  z-index: -1;
}

button:after {
  content: "";
  position: absolute;
  left: 55%;
  transform: translateX(-50%) scaleY(1) scaleX(1.45);
  top: 180%;
  width: 160%;
  height: 190%;
  background-color: #009087;
  border-radius: 50%;
  display: block;
  transition: all 0.5s 0.1s cubic-bezier(0.55, 0, 0.1, 1);
  z-index: -1;
}

button:hover {
  color: #ffffff;
  border: 1px solid #009087;
}

button:hover:before {
  top: -35%;
  background-color: #009087;
  transform: translateX(-50%) scaleY(1.3) scaleX(0.8);
}

button:hover:after {
  top: -45%;
  background-color: #009087;
  transform: translateX(-50%) scaleY(1.3) scaleX(0.8);
}
</style>