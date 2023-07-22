<template>
  <div class="wrapper">
   <div class="list-box">
      <div class="inner-shadow"></div>
      <div class="list-title">Today's tasks</div>
      <hr>

      <div id="list-items">
        <li v-for="list in lists" :key="list.id">
          <span class="title" v-bind:class="{completed: list.isComplete}">{{list.title}}</span>
        </li>
      </div>

      <input type="text" id="task-name" placeholder="task..." onsubmit="addNewTodo">
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskList',
  props: {
    msg: String,
    todos: Array
  },
  methods: {
    addNewTodo() {
      const newTodos =
        [...this.todos, 
          {
            id: this.todos.lengh, 
            text: document.getElementById('task-name').value,
            completed: false 
          }
       ];
      this.$emit('update-todos', newTodos);
    }
  },

}
</script>

<style scoped>
.wrapper {
  width: 40%;
  margin: 0 auto;
  font-size: 1.5rem;
}

.inner-shadow {
  pointer-events: none;

  width: 100%;
  height: 100%;

  position: absolute;
  top: 0;
  left: 0;
  
  -moz-box-shadow: inset 0 0 4px #000000;
  -webkit-box-shadow: inset 0 0 4px #000000;
  box-shadow: inset 0 0 4px #000000;
  
  border-radius: 48px;
}

.list-box {
  justify-content: center;
  align-items: center;
  min-height: 50vh;
  border: 2px solid #FCFCF3;
  filter: drop-shadow(0 0 2px #FCFCF3);
  border-radius: 50%;
}

.list-title {
  font-size: 1.5rem;
  font-weight: 600;
  padding: 2.5rem 0 2rem 0;
}

</style>
