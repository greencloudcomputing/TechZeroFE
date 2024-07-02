<script setup lang="ts">
import TimeseriesChart from '../components/charts/TimeseriesChart.vue'

import { ref } from 'vue'
import VueDatePicker from '@vuepic/vue-datepicker'
import '@vuepic/vue-datepicker/dist/main.css'

const startDate = ref()
const endDate = ref()
</script>

<script lang="ts">
import axios from 'axios'
import camelCaseKeys from 'camelcase-keys'

export default {
  name: 'App',
  data() {
    return {
      data: null,
      loading: true,
      errored: false
    }
  },
  mounted() {
    axios
      .get('http://localhost:8080/my_response')
      .then((response) => {
        this.data = camelCaseKeys(response.data)
      })
      .catch((error) => {
        console.log(error)
        this.errored = true
      })
      .finally(() => (this.loading = false))
  }
}
</script>

<template>
  <div class="functionView">
    <header><h1>My favourite function</h1></header>
    <div class="timeSelectContainer">
      <div>
        Start date
        <div class="datePickerContainer"><VueDatePicker v-model="startDate"></VueDatePicker></div>
      </div>
      <div>
        End date
        <div class="datePickerContainer"><VueDatePicker v-model="endDate"></VueDatePicker></div>
      </div>
    </div>
    <section v-if="errored">
      <p>Something went wrong :(</p>
    </section>
    <section class="graphSection" v-else>
      <div v-if="loading">Loading...</div>

      <div class="chartContainer" v-else>
        <TimeseriesChart :data="camelCaseKeys(data.timeseries)" />
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
