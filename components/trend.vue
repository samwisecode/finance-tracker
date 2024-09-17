<script lang="ts" setup>
interface TrendProps {
  title: string;
  amount: number;
  lastAmount: number;
  loading: boolean;
}

const props = defineProps<TrendProps>();

const trendingUp = computed(() => props.amount > props.lastAmount);

const icon = computed(() =>
  trendingUp.value
    ? 'i-heroicons-arrow-trending-up'
    : 'i-heroicons-arrow-trending-down'
);

const percentageTrend = computed(() => {
  if (props.amount === 0 || props.lastAmount === 0) return 0;
  const biggerAmount = Math.max(props.amount, props.lastAmount);
  const smallerAmount = Math.min(props.amount, props.lastAmount);
  const ratio = ((biggerAmount - smallerAmount) / smallerAmount) * 100;
  return Math.ceil(ratio);
});

const { currency } = useUseCurrency(props.amount);
</script>

<template>
  <div class="font-bold text-gray-900 dark:text-white mb-2">
    <div class="font-bold" :class="{ green: trendingUp, red: !trendingUp }">
      {{ props.title }}
    </div>
    <USkeleton class="h-8 w-full" v-if="props.loading" />
    <div v-else>
      {{ currency }}
    </div>
    <USkeleton class="h-8 w-full" v-if="props.loading" />
    <div v-else class="flex space-x-1 items-center text-sm">
      <UIcon
        :name="icon"
        class="h-6 w-6"
        :class="{ green: trendingUp, red: !trendingUp }"
      />
      <div class="text-gray-500 dark:text-gray-400">
        {{ percentageTrend }}% vs last period
      </div>
    </div>
  </div>
</template>

<style scoped>
.green {
  @apply text-green-600 dark:text-green-400;
}

.red {
  @apply text-red-600 dark:text-red-400;
}
</style>
