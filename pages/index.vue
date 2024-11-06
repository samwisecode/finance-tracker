<script lang="ts" setup>
import { ref, computed } from 'vue';
import { transactionViewOptions } from '~/constants';
const selectedView = ref(transactionViewOptions[0]);

const supabase = useSupabaseClient();

const transactions = ref<any[]>([]);

const { data } = await useAsyncData('transactions', async () => {
  const { data, error } = await supabase.from('transactions').select();
  if (error) return [];
  return data;
});

transactions.value = data.value || [];

const transactionsGroupedByDate = computed(() => {
  let groupedTransactions: Record<string, any[]> = {};
  for (const transaction of transactions.value) {
    const date = new Date(transaction.date_created).toISOString().split('T')[0];
    if (!groupedTransactions[date]) {
      groupedTransactions[date] = [];
    }
    groupedTransactions[date].push(transaction);
  }
  return groupedTransactions;
});

const { currency } = useCurrency(transactions.value[0].amount);
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
    <Transaction
      v-for="(transaction, index) in transactions"
      :key="index"
      :transaction="transaction"
    />
  </section>
</template>

<style></style>
