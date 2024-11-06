<script lang="ts" setup>
interface Transactions {
  date: string;
  transactions: any[];
}

const props = defineProps<{
  transactions: Transactions;
}>();

const dailyAmount = computed(() => {
  let amount = 0;
  for (const transaction of props.transactions.transactions) {
    if (transaction.type === 'income') {
      amount += transaction.amount;
    } else {
      amount -= transaction.amount;
    }
  }
  return amount;
});

const { currency } = useCurrency(dailyAmount.value);
</script>

<template>
  <div
    class="grid grid-cols-2 py-4 border-b border-gray-200 dark:border-gray-700"
  >
    <div class="flex items-center justify-between">
      {{ props.transactions.date }}
    </div>
    <div class="flex items-center justify-end space-x-2"></div>
  </div>
</template>

<style></style>
