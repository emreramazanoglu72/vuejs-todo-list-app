<template>
  <div class="container mt-4 pt-4">
    <div class="card">
      <div class="card-body">
        <h4 class="card-title">Yapılacaklar Listesi</h4>
        <input
          type="text"
          class="form-control"
          v-on:keyup.enter="addTodo"
          v-model="todo_name"
        />
        <button class="btn btn-dark w-100 mt-4" @click="addTodo">
          Ekle
        </button>
      </div>
      <ul class="list-group list-group-flush">
        <li
          v-for="item in list"
          :key="{ item }"
          class="list-group-item d-flex justify-content-between text-center font-weight-bold "
          v-bind:class="[
            item.status == 'deleted'
              ? 'text-danger'
              : item.status == 'success'
              ? 'text-success'
              : '',
          ]"
        >
          {{ item.name }}
          <span>
            <button
              class="btn btn-success font-weight-bold mr-2"
              @click="successTodo(item)"
            >
              ✓
            </button>
            <button
              class="btn btn-danger font-weight-bold"
              @click="deleteTodo(item)"
            >
              X
            </button>
          </span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      list: [],
      todo_name: "",
    };
  },
  methods: {
    addTodo() {
      if (this.todo_name.length > 1) {
        var count = this.list.length > 0 ? this.list[this.list.length -1].id  : 1;
        this.list.push({
          id: count + 1,
          name: this.todo_name,
          status: false,
        });
        this.todo_name = "";
      }
    },
    deleteTodo(item) {
      console.log(this.list);
      this.list.filter(
        (filter) => filter.id == item.id && (filter.status = "deleted")
      );
    },
    successTodo(item) {
      this.list.filter(
        (filter) => filter.id == item.id && (filter.status = "success")
      );
    },
  },
};
</script>
