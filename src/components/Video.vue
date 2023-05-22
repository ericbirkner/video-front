<script setup>
defineProps({
  data: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <div :title="data.title" class="video mb-3" :style="{ 'background-image': 'url(' + data.image + ')' }">
      <div class="duration">{{data.duration}}</div>
      <div class="delete" @click="$parent.deleteVideo(data.vid)">X</div>  
  </div>
</template>

<style scoped>

</style>
