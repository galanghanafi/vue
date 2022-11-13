<script>
let id = 0;
export default {
  data() {
    return {
      // hello
      message: "Hello World!",

      // counter
      counter: {
        count: 0,
      },

      // text
      titleClass: "title",
      text: "",

      // toogle
      awesome: true,

      // todo
      hideCompleted: false,
      todos: [
        { id: id++, text: "Learn HTML", status: true },
        { id: id++, text: "Learn JavaScript", status: true },
        { id: id++, text: "Learn Vue", status: false },
      ],
    };
  },

  computed: {
    filteredTodos() {
      return this.hideCompleted
        ? this.todos.filter((t) => !t.status)
        : this.todos;
    },
  },

  methods: {
    // counter
    increment() {
      this.counter.count++;
    },

    // toogle
    toogle() {
      this.awesome = !this.awesome;
    },

    // todo
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo, status: "" });
      this.newTodo = "";
    },
    removeTodo(sid) {
      this.todos.splice(sid, 1);
    },
  },
};
</script>

<template>
  <!-- 1 -->
  <div class="text-center p-5">
    <h1 class="text-lg font-black pb-2">1</h1>
    <button @click="increment" class="btn w-64 rounded-full">+1 Counter</button>
    <div :class="titleClass" class="flex flex-row justify-center">
      <p>counter:</p>
      <p class="">{{ counter.count }}</p>
    </div>
  </div>

  <!-- 2 -->
  <div class="text-center p-5">
    <h1 class="text-lg font-black pb-2">2</h1>
    <input
      v-model="text"
      type="text"
      placeholder="Type here"
      class="input input-bordered w-full max-w-xs"
    />
    <p>{{ text }}</p>
    <!-- It Doing The Same -->
    <!-- <p v-text="text"></p> -->
  </div>

  <!-- 3 -->
  <div class="text-center p-5">
    <h1 class="text-lg font-black pb-2">3</h1>
    <button @click="toogle" class="btn w-64 rounded-full">Toogle</button>
    <h1 v-if="awesome">Vue is Awesome!</h1>
    <h1 v-else>Oh no 😭</h1>
  </div>

  <!-- 4 -->
  <div class="text-center p-5">
    <h1 class="text-lg font-black pb-2">4</h1>
    <!-- form -->
    <div class="flex justify-evenly">
      <form @submit.prevent="addTodo" class="input input-bordered h-auto px-0">
        <input v-model="newTodo" type="text" class="input" />
        <button class="btn">Add Todo</button>
      </form>
      <button
        @click="hideCompleted = !hideCompleted"
        class="btn mt-0.5 rounded-full absolute right-0 mr-5"
        style="width: 100px"
      >
        {{ hideCompleted ? "showall" : "Hide Completed" }}
      </button>
    </div>
    <!-- table -->
    <div class="overflow-x-auto w-full mt-6">
      <table class="table w-full">
        <!-- head -->
        <thead>
          <tr>
            <th class="w-0">
              <label> status </label>
            </th>
            <th class="">Job</th>
            <th class="w-0">Remove</th>
          </tr>
        </thead>
        <tbody>
          <!-- todos -->
          <tr v-for="i in filteredTodos" :key="i.id">
            <th class="text-center">
              <!-- <input
                v-if="i.status"
                v-model="i.status"
                checked
                type="checkbox"
                class="checkbox"
              /> -->
              <input v-model="i.status" type="checkbox" class="checkbox" />
            </th>
            <td>
              <p>{{ i.text }}</p>
            </td>

            <td class="text-center m-0">
              <button @click="removeTodo(sid)" class="">❌</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style>
.title {
  color: red;
}
</style>
