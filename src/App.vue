<template>
  <div id="app">
    <b-row>
      <b-col>
        <b-container>
          <b-form-group horizontal :label-cols="4" label="TO DO">
            <b-form-input :class="{red:inputtext.length<10}" v-model.trim="inputtext"></b-form-input>
            <hr>
            <b-button
              v-bind:disabled="inputtext.length<10"
              v-on:click="addTodo"
              variant="outline-primary"
            >Button</b-button>
          </b-form-group>
          <ul>
            <HelloWorld
              v-for="(todo,index) in todos"
              :key="index"
             
              :motor="todo.name"
            :dana="todo.isCompleted"
              v-on:btnemitter="remover(index)"
              v-on:liemitter="liemit(index)"
            />
          </ul>
          <p v-if="istodo">there is no todo</p>
        </b-container>
      </b-col>
    </b-row>
  </div>
</template>
<script>
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",
  components: {
    HelloWorld
  },
  data: function() {
    return {
      inputtext: "",
      istodo: false,
      active: true,
      todos: [
        {
          name: "one",
          isCompleted: false
        },
        {
          name: "two",
          isCompleted: true
        },
        {
          name: "three",
          isCompleted: true
        },
        {
          name: "four",
          isCompleted: false
        }
      ]
    };
  },
  methods: {
    addTodo: function() {
      this.istodo = false;
      this.todos.push({ name: this.inputtext, isCompleted: false });
      this.inputtext=""
    },
    remover: function(index) {
      //this.todos.splice(index, 1);

      this.todos.splice(index, 1);

      if (this.todos.length === 0) {
        console.log("222");
        this.istodo = true;
      }

      console.log(this.todos.length);
    },
    jsoner: function() {
      fetch("https://jsonplaceholder.typicode.com/todos/?_limit=20")
        .then(response => response.json())
        .then(json => {
          json.forEach((el, index) => {
            this.todos.push({ name: el.title, isCompleted: false });
            //console.log(this.todos);
          });
        });
    },
    liemit: function(index) {
      this.todos[index].isCompleted = !this.todos[index].isCompleted
    }
  },
  mounted: function() {
    this.jsoner();
  }
};
</script>

<style>
.red {
  border: 2px solid red;
}
</style>
