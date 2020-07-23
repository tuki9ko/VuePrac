<template>
  <div>
    {{ msg }}
    <form>
      <button type="button" @click="addTodo()">ADD TASK</button>
      <button>FINISHED TASKS</button>
      <p>input: <input type="text" v-model="newTodo"></p>
      <p>task: {{ newTodo }}</p>
    </form>
    <div class="task-list">
      <label class="task-list__item" v-for="todo in todos" v-bind:key="todo.id">
        <input type="checkbox"><button>EDIT</button>{{ todo.text }}
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      todos: [
        {
          id: 0,
          text: 'vue-router',
          done: false
        },
        {
          id: 1,
          text: 'vuex',
          done: false
        },
        {
          id: 2,
          text: 'vue-loader',
          done: false
        },
        {
          id: 3,
          text: 'awesome-vue',
          done: true
        }
      ],
      newTodo: ""
    }
  },
  methods: {
    addTodo: function() {
      let text = this.newTodo && this.newTodo.trim();
      let newId = Math.max.apply(null, this.todos.map(n => n.id)) + 1;
      if(!text){
        return;
      }
      this.todos.push({
        id: newId,
        text: text,
        done: false
      });
      this.newTodo = '';
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@mixin flex-vender() {
  display: flex;
  display: -webkit-flex;
  display: -moz-flex;
  display: -ms-flex;
  display: -o-flex;
}

.task-list {
  @include flex-vender;
  flex-direction: column;
  align-items: center;
  &__item {
    width: 270px;
    text-align: left;
    $element: #{&};
    &--checked {
      @extend #{$element};
      color: #85a6c6;
    }
  }
}
</style>
