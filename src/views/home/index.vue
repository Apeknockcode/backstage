<template>
  <div>
    <!-- search -->
    <a-divider class="line" />
    <!-- chart -->
    <a-row :gutter="24">
      <a-col :span="12">
        <a-card :bordered="false">
          <DataOverview />
        </a-card>
      </a-col>
      <a-col :span="12">
        <a-card :bordered="false">
          <TradingHistory :loading="loading" />
        </a-card>
      </a-col>
    </a-row>
    <a-divider class="line" />
    <Table :url="fetchApi.list" :columns="columns" :hiddenFilter="true" :scroll="{ x: 1200 }" />
  </div>
</template>
<script setup lang="ts">
  import DataOverview from './components/DataOverview.vue';
  import TradingHistory from './components/TradingHistory.vue';
  import { columns } from './constant';
  import fetchApi from '/@/api/home';
  import { useHomeStore } from '/@/store/modules/home';

  const store = useHomeStore();
  const loading = ref(false);

  onMounted(async () => {
    loading.value = true;
    await store.fetchInfo();
    loading.value = false;
  });

  onUnmounted(() => {
    store.resetState();
  });
</script>
<style lang="less" scoped>
  .search {
    & :deep(.ant-input) {
      height: 48px;
    }
  }
</style>
