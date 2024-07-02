<script setup lang="ts">
import TimeseriesChart from '../components/charts/TimeseriesChart.vue'

import { ref, watch } from 'vue'
import VueDatePicker from '@vuepic/vue-datepicker'
import '@vuepic/vue-datepicker/dist/main.css'
import { startOfDay } from 'date-fns'

import axios from 'axios'
import camelCaseKeys from 'camelcase-keys'

const now = new Date()
const startDate = ref(startOfDay(now))
const endDate = ref(now)
const dateFormat = 'dd/MM/yyyy HH:mm'

const data = ref(null)
const loading = ref(true)
const errored = ref(false)

const fetchData = () => {
  if (startDate.value >= endDate.value) {
    return
  }

  loading.value = true
  errored.value = false

  axios
    .get(
      `http://localhost:8080/energy?from=${startDate.value.toISOString()}&to=${endDate.value.toISOString()}&functionId=667aa0c384809f8a29ddc2f9`
    )
    .then((response) => {
      data.value = camelCaseKeys(response.data)
    })
    .catch((error) => {
      console.log(error)
      errored.value = true
    })
    .finally(() => {
      loading.value = false
    })
}

watch([startDate, endDate], fetchData)

// Fetch initial data
fetchData()
</script>

<template>
  <div class="functionView">
    <header><h1>My favourite function - 667aa0c384809f8a29ddc2f9</h1></header>
    <div class="timeSelectContainer">
      <div>
        Start date
        <div class="datePickerContainer">
          <VueDatePicker v-model="startDate" :format="dateFormat"></VueDatePicker>
        </div>
      </div>
      <div>
        End date
        <div class="datePickerContainer">
          <VueDatePicker v-model="endDate" :format="dateFormat"></VueDatePicker>
        </div>
      </div>
    </div>
    <section v-if="errored">
      <p>Something went wrong :(</p>
    </section>
    <section class="graphSection" v-else>
      <div v-if="loading">Loading...</div>

      <div class="chartContainer" v-else>
        <TimeseriesChart :data="data" />
      </div>
    </section>
  </div>
</template>

<style>
.chartContainer {
  background-color: white;
  border-radius: 10px;
  margin: 10px;
}

.timeSelectContainer {
  background-color: white;
  display: flex;
  gap: 5px;
  padding: 10px;
  padding-top: 5px;
  border-bottom: 1px solid rgb(222, 222, 222);
  flex: content;
  flex-direction: row;
}

.datePickerContainer {
  width: 200px;
}

header {
  background-color: white;
  padding-left: 10px;
  border-bottom: 1px solid rgb(222, 222, 222);
}
</style>
