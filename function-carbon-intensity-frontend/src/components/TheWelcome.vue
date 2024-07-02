<script setup lang="ts">
import MetricItem from './MetricItem.vue'
import Header from './Header.vue'

</script>

<template>
  <div class="header">
    <Header>
      <template #heading>GreenCloud Server Energy Reporting</template>
    </Header>
  </div>

  <div class="grid-container">
    <MetricItem>
      <template #icon>
        <DocumentationIcon />
      </template>
      <template #heading>Total Time Taken</template>

      Metric 1 placeholder
    </MetricItem>

    <MetricItem>
      <template #icon>
        <ToolingIcon />
      </template>
      <template #heading>Electricity Consumed</template>
      Metric 2 placeholder
    </MetricItem>

    <MetricItem>
      <template #icon>
        <EcosystemIcon />
      </template>
      <template #heading>Total Cost</template>
      Metric 3 placeholder
    </MetricItem>

    <MetricItem>
      <template #icon>
        <SupportIcon />
      </template>
      <template #heading>Carbon Intensity</template>

      Metric 4 placeholder
    </MetricItem>

  </div>

</template>

<style>
.grid-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  padding: 20px;
}
</style>

