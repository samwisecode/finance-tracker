<script lang="ts" setup>
const { currency } = useUseCurrency(3000);

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
        <UIcon name="i-heroicons-arrow-up-right" class="text-green-600" />
        <div>Salary</div>
      </div>
      <div>
        <UBadge color="gray" variant="outline" size="sm">Entertainment</UBadge>
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
            <UIcon name="i-heroicons-dots-vertical" />
          </UButton>
        </UDropdown>
      </div>
    </div>
  </div>
</template>

<style></style>
