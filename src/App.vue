<template>
  <div id="todoMain">
    <h1>{{title}}</h1>
    <input type="text" class="nes-input" placeholder="Add todo..." v-on:keyup.enter="addTodo">
    <ul>
      <li v-bind:key="todo" v-for="todo in todos" class="flex">
        <label>
          <input type="checkbox" class="nes-checkbox" v-model="todo.done">
          <span>&nbsp;</span>
        </label>
        <del v-if="todo.done">{{todo.text}}</del>
        <span v-else>{{todo.text}}</span>
        <div class="space"></div>
        <button class="nes-btn is-error padding" v-on:click="removeTodo(todo.id)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'app',
  data: () => {
    return {
      title: 'TODOS',
      todos: [
      ],
    }
  },
  components: {
  },
  methods: {
    addTodo(event) {
      const text = event.target.value;
      this.todos.push({text, done: false, id: Date.now()});
      event.target.value = '';
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    check(todo) {
      todo.done = !todo.done
    }
  }
}
</script>

<style>
html,
body,
pre,
code,
kbd,
samp {
  font-family: "Press Start 2P";
}

body {
  background: #20262E;
  padding: 20px;
}

#todoMain {
  background: #fff;
  border-radius: 4px;
  padding: 20px;
  transition: all 0.2s;
}

li {
  margin: 8px 0;
}

del {
  color: rgba(0, 0, 0, 0.3);
}

.padding {
  padding: 1px 7px 2px;
}

.flex {
  display: flex;
}

.space {
  flex-grow: 1;
}

</style>
