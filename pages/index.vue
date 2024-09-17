<script lang="ts" setup>
import { ref } from 'vue';
import { transactionViewOptions } from '~/constants';
const selectedView = ref(transactionViewOptions[0]);
</script>

<template>
  <section class="flex items-center justify-between mb-5">
    <h1 class="text-2xl font-bold">Summary</h1>
    <USelectMenu v-model="selectedView" :options="transactionViewOptions" />
  </section>
  <section
    class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 sm:gap-8 mb-10"
  >
    <Trend
      title="Income"
      :amount="30000"
      :lastAmount="22000"
      :loading="false"
    />
    <Trend
      title="Expenses"
      :amount="1000"
      :lastAmount="2000"
      :loading="false"
    />
    <Trend
      title="Investments"
      :amount="4000"
      :lastAmount="3000"
      :loading="false"
    />
    <Trend
      title="Savings"
      :amount="30000"
      :lastAmount="26000"
      :loading="false"
    />
  </section>

  <section>
    <h1 class="text-xl font-bold">Transactions</h1>
    <Transaction />
    <Transaction />
    <Transaction />
    <Transaction />
    <Transaction />
    <Transaction />
    <Transaction />
  </section>
</template>

<style></style>
