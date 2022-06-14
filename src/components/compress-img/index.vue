<template>
  <div class="ci-box">
    <div id="dragBox" class="drag-box">
      <ul>
        <li v-for="item of files" :key="item.lastModified">{{ item.name }}</li>
      </ul>
    </div>
    <div class="upload-button">上传</div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onBeforeUnmount, onMounted, ref } from "vue";
export default defineComponent({
  setup() {
    let count = 0;
    let files = ref<FileList>();
    function handleDrag(e: DragEvent) {
      e.stopPropagation();
      e.preventDefault();
      return false;
    }
    function handleDrop(e: DragEvent) {
      e.stopPropagation();
      e.preventDefault();
      if (e?.dataTransfer?.files) {
        files.value = e?.dataTransfer?.files;
      } else {
        files.value = undefined;
      }
      return false;
    }
    function documentDrag(e: DragEvent) {
      e.stopPropagation();
      e.preventDefault();
      return false;
    }
    onMounted(() => {
      document.addEventListener("dragover", documentDrag, false);
      document.addEventListener("drop", documentDrag, false);
      document.addEventListener("dragenter", documentDrag, false);

      const dragBox = document.getElementById("dragBox");
      dragBox?.addEventListener("dragover", handleDrag, false);
      dragBox?.addEventListener("drop", handleDrop, false);
      dragBox?.addEventListener("dragenter", handleDrag, false);
    });
    onBeforeUnmount(() => {
      document.removeEventListener("dragover", documentDrag, false);
      document.removeEventListener("drop", documentDrag, false);
      document.removeEventListener("dragenter", documentDrag, false);

      const dragBox = document.getElementById("dragBox");
      dragBox?.removeEventListener("dragover", handleDrag, false);
      dragBox?.removeEventListener("drop", handleDrop, false);
      dragBox?.removeEventListener("dragenter", handleDrag, false);
    });
    return { count, handleDrag, files };
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
  .upload-button {
    display: inline-block;
    padding: 10px;
    // border: 1px solid blue;
    background: burlywood;
    color: #fff;
    border-radius: 4px;
    margin-top: 10px;
  }
}
</style>
