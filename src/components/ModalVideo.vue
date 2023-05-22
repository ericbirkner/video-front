
<script>
import { reactive, toRefs, computed, onMounted, ref} from "vue";
export default{
  props: {
    video: {
      type: Object,
      required: true
    }
  },
  setup(props,ctx) {
    const state = reactive({
      show: false
    });    

    onMounted(() => {
        console.log('componente ModalVideo');
    });

    return {
      state
    };
    
  }
}
</script>

<template>
  <div class="modal fade show d-block oscuro modal-video" tabindex="1">
        <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable modal-xl">
          <div class="modal-content gris">
            <div class="modal-header">
              <button @click="$parent.state.showModalVideo=false" type="button" class="btn-close" data-bs-dismiss="modal" aria-label="cerrar ventana"></button>
            </div>
            <div class="modal-body container">
              <div class="row align-items-center">
                <div class="col-12 col-md-6">
                  
                  <iframe v-if="state.show" width="100%" height="315" :src="'https://www.youtube.com/embed/'+video.vid+'?autoplay=1'" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
                  
                  <div v-else class="preview">
                    <img :src="video.image" :alt="video.title" class="thumbnail">
                    <div class="play" @click="state.show=true"></div>
                    <div class="duration">{{video.duration}}</div>
                  </div>
                  
                  
                </div>
                <div class="col-12 col-md-6">
                  <h4>{{video.title}}</h4>
                  <div class="description-modal">{{video.description}}</div>
                </div>
              </div>
            </div>
            <div class="modal-footer"></div>
          </div>
        </div>
  </div>
</template>

<style scoped>
</style>
