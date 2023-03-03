<template>
  <div class="hello">
    <TodoTemplate v-if="!deleted" :msg="msg"/>
    <h1>{{ msg }}</h1>
    <button v-on:click="del()"></button>
  </div>
</template>

<script>
import TodoTemplate from './TodoTemplate.vue';
export default {
  name: 'HelloWorld',
  data: ()=>({
    deleted: false
  }),
  components: {
    TodoTemplate
  },
  props: {
    msg: String
  },
  methods:{
    del(){
      this.deleted= true;
    }
  }
}
</script>
