<script setup>
defineProps({
  vid: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="modal fade show d-block oscuro" tabindex="1">
    <div class="modal-dialog modal-lg modal-dialog-centered modal-dialog-scrollable">
      <div class="modal-content gris">
        <div class="modal-header">
          <button @click="$parent.state.showConfirm=false" type="button" class="btn-close" data-bs-dismiss="modal" aria-label="cerrar ventana"></button>
        </div>
        <div class="modal-body">
          <div class="mb-3"><h5>¿Seguro que quieres eliminar este video?</h5></div>
          <div class="text-end">
            <button type="button" class="btn btn-outline-primary me-2 me-md-3 ps-md-4 pe-md-4 ps-lg-5 pe-lg-5" @click="$parent.state.showConfirm=false">Cancelar</button>
            <button type="button" class="btn btn-primary ps-md-4 pe-md-4 ps-lg-5 pe-lg-5" @click="$parent.deleteVideo">Eliminar</button>
          </div>
        </div>
        <div class="modal-footer"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
