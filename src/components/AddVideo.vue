<script>

function YouTubeGetID(url){
   url = url.split(/(vi\/|v=|\/v\/|youtu\.be\/|\/embed\/)/);
   return (url[2] !== undefined) ? url[2].split(/[^0-9a-z_\-]/i)[0] : url[0];
}

const getVimeoIdFromUrl = (url) => {
  // Look for a string with 'vimeo', then whatever, then a
  // forward slash and a group of digits.
  const match = /vimeo.*\/(\d+)/i.exec(url);
  // If the match isn't null (i.e. it matched)
  if (match) {
    // The grouped/matched digits from the regex
    return match[1];
  }
}

import axios from 'axios';
import { reactive, toRefs, computed, onMounted, ref} from "vue";
export default{
  setup(props,ctx) {
    const state = reactive({
      url: '',
      error: false,
      repeat: false,
      source: 'youtube'
    });

    const postVideo = async () => {
        state.error = false;
        state.repeat = false;
        if(state.url){
            let vid = "";
            if (state.url.includes('youtu')){
                vid = YouTubeGetID(state.url);
            }else{
                vid = getVimeoIdFromUrl(state.url);
                state.source = "vimeo"
            }
            console.log(vid);
                
                const res = await axios.get(`http://ec2-44-210-126-6.compute-1.amazonaws.com/api/videos/${vid}`);
                console.log(res.data);
                try {
                    if(!res.data.hasOwnProperty('vid')){
                    
                        axios.post('http://ec2-44-210-126-6.compute-1.amazonaws.com/api/videos',
                            {   
                                vid:vid,
                                source:state.source
                            }
                        )
                        .then(response => {
                            console.log(response.data);
                            if(response.data.hasOwnProperty('vid')){
                                ctx.emit('callVideos');
                            }
                        }).catch(error => {
                            console.log(error)
                            state.error = true;
                        })
                    }else{
                        state.repeat = true;
                    }    
                } catch (error) {
                    console.log(error)
                    state.error = true;
                }
                
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
    <h3>Añadir nuevo video</h3>
    <div class="input-group mb-3">
        <input v-model="state.url" type="text" class="form-control" placeholder="https://www.youtube.com/watch?v=tNXOzZVIVm0">
        <button class="btn btn-primary ps-md-5 pe-md-5 anadir" type="button" id="button-addon2" @click="postVideo">Añadir</button>
    </div>
    <div v-if="state.error" class="error" role="alert">
        <small>Error al subir Url, pruebe con una correcta.</small>
    </div>
    <div v-if="state.repeat" class="error" role="alert">
        <small>El video ingresado ya existe.</small>
    </div>
</template>

<style scoped>

</style>
