<template>
  <div class="ci-box">
    <div class="drag-box" @drag="handleDrag"></div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onBeforeUnmount, onMounted } from "vue";
export default defineComponent({
  setup() {
    let count = 0;
    function handleDrag(e: DragEvent) {
      e.preventDefault();
      console.log(e);
    }
    function documentDrag(e: DragEvent) {
      e.stopPropagation();
      e.preventDefault();
    }
    onMounted(() => {
      window.addEventListener("dragover", documentDrag);
      window.addEventListener("drag", documentDrag);
    });
    onBeforeUnmount(() => {
      window.removeEventListener("dragover", documentDrag);
      window.removeEventListener("drag", documentDrag);
    });
    return { count, handleDrag };
  },
});
</script>

<style lang="less" scoped>
.ci-box {
  .drag-box {
    width: 500px;
    height: 500px;
    border: 2px dashed burlywood;
    border-radius: 4px;
  }
}
</style>
