<template>
  <CompressImg></CompressImg>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import CompressImg from "@/components/compress-img/index.vue";
export default defineComponent({
  name: "App",
  components: {
    CompressImg,
  },
});
</script>

<style lang="less"></style>
