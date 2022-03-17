<template>
  <div class="commentList">
    <h5 class="text-muted mb-4" style="text-align: left">
      <span class="badge badge-success">{{ comments.length }}</span>{{" "}}
      {{ comentarioPlural }}
    </h5>

    <div class="alert text-center alert-info" v-if="comments.length ===0 && !loading">
      Se el primero en comentar!
    </div>
    <Comentario v-for="comment in comments" :key="comment.id" :comment="comment"></Comentario>
  </div>
</template>

<script>
import Comentario from "@/components/Comentario";
export default {
  name: "CommentList",
  props: {
    comments: {
      type: Array,
      default: () => [],
    },
    loading: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    comentarioPlural() {
      const plural = this.comments.length > 1 ? 's': '';
      return 'Comentario' +  plural;
    }
  },
  components: {
    Comentario,
  }
}
</script>

<style scoped>

</style>
