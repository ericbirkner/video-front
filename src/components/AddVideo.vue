<script>

function YouTubeGetID(url){
   url = url.split(/(vi\/|v=|\/v\/|youtu\.be\/|\/embed\/)/);
   return (url[2] !== undefined) ? url[2].split(/[^0-9a-z_\-]/i)[0] : url[0];
}

import axios from 'axios';
import { reactive, toRefs, computed, onMounted, ref} from "vue";
export default{
  setup(props,ctx) {
    const state = reactive({
      url: '',
      error: false
    });

    const postVideo = () => {
        state.error = false;
        if(state.url){
            const vid = YouTubeGetID(state.url);
            console.log(vid);
            axios.post('http://ec2-44-210-126-6.compute-1.amazonaws.com/api/videos',{vid:vid})
            .then(response => {
                console.log(response.data);
                if(response.data.hasOwnProperty('vid')){
                    ctx.emit('callVideos');
                }
            }).catch(error => {
                console.log(error)
                state.error = true;
            })
        }
        
    }

    onMounted(() => {
        console.log('componente addVideo');
    });

    return {
      state,
      postVideo
    };
    
  },
  emits: ['callVideos']
}

</script>

<template>
    <h3 @click="$parent.getVideos();">Añadir nuevo video</h3>
    <div class="input-group mb-3">
        <input v-model="state.url" type="text" class="form-control" placeholder="https://www.youtube.com/watch?v=tNXOzZVIVm0">
        <button class="btn btn-primary ps-5 pe-5 anadir" type="button" id="button-addon2" @click="postVideo">Añadir</button>
    </div>
    <div v-if="state.error" class="error" role="alert">
        <small>Error al subir Url, pruebe con una correcta.</small>
    </div>
</template>

<style scoped>

</style>
