<script setup>
defineProps({
  data: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <div 
    :title="data.title" 
    class="video mb-3" 
    :style="{ 'background-image': 'url(' + data.image + ')' }"
  > 
    <img :src="data.image" class="thumbnail" @click="$parent.state.currentVideo=data;$parent.state.showModalVideo=true;">
      <div class="duration">{{data.duration}}</div>
      <div class="delete" @click="$parent.state.id=data.id;$parent.state.showConfirm=true;">X</div>  
  </div>
</template>

<style scoped>

</style>
