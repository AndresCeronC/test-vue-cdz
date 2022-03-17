<template>
<!--  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  <div class="App container bg-light shadow">
    <header class="App-header">
      <img src="./assets/logo.png" class="loadingSpin" alt="logo" />
      <h1 clas="App-title">
        Vue Comments
        <span class="px-2" role="img" aria-label="Chat">
          💬
        </span>
      </h1>
    </header>
    <div class="row">
      <div class="col-4 pt-3 border-right" style="text-align: left">
        <h6>Ingresa tu comentario</h6>
<!--        <CommentForm addComment={addComment} reloadComentarios={loadComentarios} />-->
        <CommentForm @newComment="getData"></CommentForm>
      </div>
      <div class="col-8  pt-3 bg-white">
        <CommentList :loading="loading" :comments="comments"></CommentList>
<!--        <CommentList
            loading={loading}
            comments={comments}
        />-->
      </div>
    </div>
  </div>
</template>

<script>

import CommentForm from "@/components/CommentForm";
import CommentList from "@/components/CommentList";
import axiosInstance from "./services/axiosConfig";
export default {
  name: 'App',
  data: function () {
    return {
      comments: [],
      loading: false,
    }
  },
  mounted () {
    console.log("App::mounted");
    this.getData();
  },
  methods: {
    getData() {
      this.loading = true;
      axiosInstance
        .get("/api/mensajes")
        .then((res)=> {
          console.log(res.data);
          this.comments = res.data;
        })
        .catch((err)=>{console.log(err)})
        .finally(()=>{this.loading = false})
    }
  },
  components: {
    CommentForm,
    CommentList,
  },
}
</script>


<style>
@import '~bootstrap/dist/css/bootstrap.css';
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.App {
    padding-top: 1rem;
    padding-bottom: 1rem;
    margin: 1rem auto;
}

.App-logo {
    height: 80px;
}

.Spin {
    animation: App-logo-spin infinite 2s linear;
}

.App-header {
    text-align: center;
    background-color: #37a6e7;
    padding: 20px;
    color: white;
    border-radius: 0.3rem;
}

.App-title {
    font-size: 1.5em;
}

.App-intro {
    font-size: large;
}

@keyframes App-logo-spin {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}

.form-group {
    padding-top: 4px;
    padding-bottom: 4px;
}

.badge-success {
    background-color: green;
}

</style>
