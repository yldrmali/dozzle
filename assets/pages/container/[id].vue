<template>
  <search></search>
  <log-container :id="id" show-title :scrollable="activeContainers.length > 0" v-if="currentContainer"></log-container>
  <div v-else-if="ready" class="notification is-warning is-light m-6">
    <h1 class="title">
      {{ $t("error.container-not-found") }}
    </h1>
  </div>
</template>

<script lang="ts" setup>
import search from "@/components/Search.vue";
const store = useContainerStore();
const { id } = defineProps<{ id: string }>();

const currentContainer = store.currentContainer($$(id));
const { activeContainers, ready } = storeToRefs(store);

setTitle("loading");

onMounted(() => {
  setTitle(currentContainer.value?.name);
});

watchEffect(() => setTitle(currentContainer.value?.name));
</script>
