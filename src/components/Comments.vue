<template>
  <div class="container">
    <h1>Comentários</h1>
    <hr/>
    <Formtodo v-on:add-todo="addComment"></Formtodo>
    <div class="list-group">
      <p v-if="comments.length <= 0">Sem comentários...</p>
      <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
        <span class="comment_author">Autor: <strong>{{ comment.name }}</strong></span>
        <p>{{ comment.message }}</p>
        <div>
          <a href="#" title="excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
        </div>
      </div>
    </div>
    <hr/>
  </div>

</template>

<script>
import Formtodo from "./Formtodo";

export default {
  components: {
    Formtodo
  },
  data() {
    return {
      comments: [],
     
    }
  },
  methods: {

    addComment(comment) {
      this.comments.push(comment);
    },

    removeComment(index){
      this.comments.splice(index, 1);

    }
  },
  computed: {
    allComments(){
      return this.comments.map(comment => ({
      ...comment,
      name: comment.name.trim() === '' ? 'Anonimo' : comment.name
      }))


    }
  },
  watch: {
    comments(val){
      console.log("val", val)
    }
  }

}
</script>


