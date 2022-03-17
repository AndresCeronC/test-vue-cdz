<template>
  <div class="media mb-3" style="display: flex">
    <img
        class="mr-3 bg-light rounded"
        width="48"
        height="48"
        :src="urlImg"
        :alt="comment.usuario"
    />
    <div class="media-body p-2 shadow-sm rounded bg-light border" style="flex-grow: 1; margin-left: 5px;text-align: left">
      <h6 class="mt-0 mb-1 text-muted">{{ comment.usuario }}</h6>
      {{ comment.comentario }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Comment",
  props: {
    comment: {
      type: Object,
      default: ()=>{return {}}
    }
  },
  computed: {
    urlImg() {
      return "https://ui-avatars.com/api/?name=" + this.comment.usuario;
    }
  }
}
</script>

<style scoped>

</style>
