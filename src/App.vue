<script setup>
import { ref } from "vue";
import FormField from "./components/FormField.vue";

const annualSalary = ref(0);
const weekOn = ref(1);
const weekOff = ref(1);
const dailyHour = ref(1);
const avgHourWeekly = ref(0);
const weeklyGrossPay = ref(0);
const hourlyRate = ref(0);

function calculateHourlySalary() {

  const _weekOn = weekOn.value
  const _weekOff = weekOff.value
  const _dailyHour = dailyHour.value
  const _annualSalary = annualSalary.value

  const _avgHourWeekly = (_weekOn * _dailyHour * 7) / (_weekOn + _weekOff)
  avgHourWeekly.value = _avgHourWeekly.toFixed(2);
  const _weeklyGrossPay = _annualSalary / 52.143;
  weeklyGrossPay.value = _weeklyGrossPay.toFixed(2);
  const _hourlyRate = (_weeklyGrossPay/_avgHourWeekly).toFixed(2)
  hourlyRate.value = _hourlyRate
}

</script>

<template>
  <title>Hahaha</title>
  <form @submit.prevent="calculateHourlySalary()" class="max-w-md mx-auto">
    <FormField label="annual salary">
      Annual Salary
      <input
        type="number"
        v-model="annualSalary"
        class="border border-black rounded"
      />
    </FormField>
    <FormField label="annual salary">
      Week On:
      <input
        type="number"
        v-model="weekOn"
        class="border border-black rounded"
      />
    </FormField>
    <FormField label="annual salary">
      Week off:
      <input
        type="number"
        v-model="weekOff"
        class="border border-black rounded"
      />
    </FormField>

    <FormField label="annual salary">
      Daily Hour:
      <input
        type="text"
        v-model="dailyHour"
        class="border border-black rounded"
      />
    </FormField>

    <button type="submit" class="border rounded">Calculate</button>
  </form>

  <p>Annual Salary: AU${{ annualSalary.toLocaleString() }}</p>
  <p>Week On: {{ weekOn}}</p>
  <p>Week Off: {{ weekOff}}</p>
  <p>Hours of Work / Day: {{ dailyHour }}</p>

  <p>Average hours work / week: {{ avgHourWeekly }}</p>
  <p>Weekly gross pay: AU${{ weeklyGrossPay.toLocaleString() }}</p>
  <p>Hourly rate: AU${{ hourlyRate.toLocaleString() }}</p>
</template>
