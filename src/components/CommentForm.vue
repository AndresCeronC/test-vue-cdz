<template>
  <form method="post" @submit="onSubmit">
    <div class="form-group">
      <input
          v-model="comment.usuario"
          class="form-control"
          placeholder="😎 Tu nombre"
          type="text"
      />
    </div>
    <div class="form-group">
      <textarea
          v-model="comment.comentario"
          class="form-control"
          placeholder="🤬 Tu comentario"
          rows="5"
      />
    </div>
    <div className="alert alert-danger" v-if="error !== ''">{{ error }}</div>
<!--    {renderError()}-->
    <div class="form-group">
      <button :disabled="loading" class="btn btn-primary">
        Comentar &#10148;
      </button>
    </div>
  </form>
</template>

<script>
import axiosInstance from '@/services/axiosConfig';
export default {
  name: "CommentForm",
  emits: ['newComment'],
  data: function () {
    return {
      comment: {
        usuario: '',
        comentario: '',
      },
      loading: false,
      error: '',
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      console.log('onSubmit', this.comment);
      if (!this.isFormValid()) {
        this.error = "Todos los campos son requeridos";
        return;
      }
      this.error = "";
      this.loading = true;
      axiosInstance
          .post('/api/mensajes/', this.comment)
          .then((res) => {
            console.log('respuesta', res.status);
            this.comment = { usuario: "", comentario: "" };
            this.$emit('newComment');
          })
          .catch((err) => {
            console.log(err);
            this.error = "Error al enviar el comentario.";
          })
          .finally(()=>{this.loading = false})
    },
    isFormValid () {
      return this.comment.usuario !== "" && this.comment.comentario !== "";
    }
  }
}
</script>

<style scoped>

</style>
