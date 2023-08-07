<template>
  <div class="wrapper" @keydown="toggleSelection">
    <div class="list-box">
      <div class="inner-shadow"></div>
      <div class="list-title">Today's tasks</div>
      <hr />

      <div id="list-items" ref="todosContainer" v-if="todos.length">
        <li
          v-for="(todo, index) in todos"
          :key="todo.id"
          :class="{ selected: index === selectedIndex, completed: todo.completed}"
        >
          <span class="todo-item" @click="toggleCompleteTodo(todo, index)">
            {{ todo.text }}
          </span>
        </li>
      </div>

      <input
        type="text"
        id="task-name"
        placeholder="task..."
        @keydown.enter="addNewTodo"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "TaskList",
  props: ["todos"],
  data() {
    return {
      selectedIndex: null,
    };
  },
  mounted() {
    document.addEventListener("keydown", this.toggleSelection);
  },
  methods: {
    addNewTodo() {
      if (!document.getElementById("task-name").value) return;
      const newTodos = [
        ...this.todos,
        {
          id: this.todos.lengh || 0,
          text: document.getElementById("task-name").value,
          completed: false,
        },
      ];

      const input = document.getElementById("task-name");

      input.value = "";
      input.focus();

      this.$emit("update-todos", newTodos);

      setTimeout(() => {
        this.scrollToListEnd();
      }, 250);
    },

    toggleCompleteTodo(todo, index) {
      const todoIndex = index;
      const isCompleted = todo.completed;

      const updatedTodos = this.todos;
      updatedTodos[todoIndex].completed = !isCompleted;

      this.$emit("update-todos", updatedTodos);
    },
    
    scrollToListEnd() {
      const container = this.$refs.todosContainer;
      const lastTodo = container.querySelector("li:last-child");
      if (lastTodo) {
        lastTodo.scrollIntoView({ behavior: "smooth", block: "end" });
      }
    },

    toggleSelection(event) {
      if (this.todos.length === 0) return;

      const input = document.getElementById("task-name");
      const listItems = document.querySelectorAll("#list-items li");

      if (input != document.activeElement) {
        const isTooglingCompleteness = event.code === "Space" || event.key === "Enter";
        if (isTooglingCompleteness) {
          event.preventDefault();
          const todo = this.todos[this.selectedIndex];

          this.toggleCompleteTodo(todo, this.selectedIndex);
          return;
        }
      }

      if (event.key === "Enter") return;
      if (event.key === "Escape" || event.key === "Tab") {
        listItems.forEach((item) => item.classList.remove("selected"));
        this.selectedIndex = null;
        setTimeout(() => { input.focus(); }, 100);
      }

      if (event.key === "ArrowUp" || event.key === "ArrowDown") {
        input.blur();
        const goingUp = event.key === "ArrowUp";

        if (this.selectedIndex === null) {
          this.selectedIndex = goingUp ? this.todos.length : 0;
        } else {
          this.selectedIndex =
            goingUp ? 
              this.selectedIndex === 0 ? 
                this.todos.length - 1 
              : 
                this.selectedIndex - 1
            :
              this.selectedIndex === this.todos.length - 1 ?
                0
              :
                this.selectedIndex + 1;
        }
      }
    },
  },

  watch: {
    selectedIndex(newIndex) {
      const listItems = document.querySelectorAll("#list-items li");
      listItems.forEach((item) => item.classList.remove("selected"));

      if (newIndex !== null) {
        listItems[newIndex]?.classList.add("selected");
        setTimeout(() => {
          document.querySelector(".selected")?.scrollIntoView({ behavior: "smooth", block: "end" })
        }, 100)
      }
    },
  },
};
</script>

<style scoped>
.wrapper {
  min-width: 100%;
  
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
  margin: 0 auto;
  justify-content: center;
  align-items: center;
  min-height: 50vh;
  max-width: 650px;
  filter: drop-shadow(0 0 2px #fcfcf3);
  border-radius: 48px;
  overflow: hidden;
}

.list-title {
  font-size: 1.5rem;
  font-weight: 600;
  padding: 2.5rem 0 2rem 0;
}

.selected > .todo-item > span {
  text-decoration: underline !important;
}

.selected > .todo-item {
  text-decoration: underline !important;
}

.selected.completed > .todo-item {
  background-color: #ffcbad57;
  transition: all 0.2s;
}

.completed {
  text-decoration: line-through;
}

.todo-item {
  text-decoration: underline #00000000;
  word-wrap: break-word;
  animation: strike 0.25s linear;
  transition: all 0.5s;
}

.completed .todo-item:after {
  display: inline-block;
  content: "⛔";
}

.todo-item:after {
  display: inline-block;
  padding-left: 8px;
  font-size: 16px;
  content: "✅";
}

#list-items {
  max-height: 55vh;
  overflow-y: scroll;
}

#list-items li {
  padding: 4px 0;
}

::-webkit-scrollbar {
  width: 7px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
}

::-webkit-scrollbar-thumb {
  background: #888;
}


@keyframes strike {
  from { 
    text-decoration-color: transparent; 
  }
  to { 
    text-decoration-color: #000; 
  }
}

</style>
