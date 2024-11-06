<script lang="ts" setup>
interface Transaction {
  id: number;
  amount: number;
  date_created: string;
  description?: string;
  type?: string;
  category?: string;
}

const props = defineProps<{
  transaction: Transaction;
}>();

const { currency } = useCurrency(props.transaction.amount);

const isIncome = computed(() => props.transaction.type === 'Income');

const arrowIcon = computed(() =>
  isIncome.value ? 'i-heroicons-arrow-right' : 'i-heroicons-arrow-left'
);

const arrowIconColor = computed(() =>
  isIncome.value ? 'text-green-600' : 'text-red-600'
);

const items = [
  [
    {
      label: 'Edit',
      icon: 'i-heroicons-pencil',
      click: () => console.log('Edit Transaction'),
    },
    {
      label: 'Delete',
      icon: 'i-heroicons-trash',
      click: () => console.log('Transaction Deleted'),
    },
  ],
];
</script>

<template>
  <div
    class="grid grid-cols-2 py-4 border-b border-gray-200 dark:border-gray-700"
  >
    <div class="flex items-center justify-between">
      <div class="flex items-center space-x-2">
        <UIcon :name="arrowIcon" :class="arrowIconColor" />
        <div>{{ props.transaction.description }}</div>
      </div>
      <div>
        <UBadge
          color="gray"
          variant="outline"
          size="sm"
          v-if="props.transaction.category"
          >{{ props.transaction.category }}</UBadge
        >
      </div>
    </div>
    <div class="flex items-center justify-end space-x-2">
      <div>{{ currency }}</div>
      <div>
        <UDropdown :items="items" placement="bottom-start">
          <UButton
            color="gray"
            variant="ghost"
            trailing-icon="i-heroicons-ellipsis-horizontal"
          >
            <UIcon name="i-heroicons-dots-horizontal" />
          </UButton>
        </UDropdown>
      </div>
    </div>
  </div>
</template>

<style></style>
