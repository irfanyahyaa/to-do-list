<template>
  <div class="list-task m-5">
    <h1>Todo List</h1>
    <div v-if="tasks.length">
      <div
        v-for="item of tasks"
        class="item-task d-flex align-items-start border-bottom pt-3 pb-4"
      >
        <input
          type="checkbox"
          name="status"
          id="task"
          class="me-2 mt-2"
          :checked="item.isDone"
        />
        <div class="d-flex flex-column">
          <div
            class="title-task mb-2"
            :class="{ 'completed-task': item.isDone }"
          >
            {{ item.title }}
          </div>
          <div class="description-task small text-mutes">
            {{ item.description }}
          </div>
          <a href="#" @click="deleteTask(item)">Delete</a>
        </div>
      </div>
    </div>
    <div v-else>Belum ada task</div>
    <div class="action py-2">
      <a
        href="#"
        class="add-button"
        v-if="!isCreating"
        @click="isCreating = !isCreating"
        >Add Task</a
      >
      <div class="add-card" v-else>
        <div class="card mb-2">
          <div class="card-body d-flex flex-column p-0">
            <input
              v-model="titleValue"
              class="form-control border-0 mb-2"
              placeholder="Title"
              type="text"
            />
            <textarea
              v-model="descriptionValue"
              class="form-control border-0 small"
              placeholder="Description"
              rows="3"
            ></textarea>
          </div>
        </div>
        <div class="button-wrapper d-flex">
          <button class="btn btn-primary me-2" @click="saveTask">Save</button>
          <button class="btn btn-outline-secondary" @click="clearForm">
            Cancel
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";

export default {
  data() {
    return {
      // daftar task
      tasks: [],
      // Status saat menambahkan task
      isCreating: false,
      titleValue: "",
      descriptionValue: "",
    };
  },
  methods: {
    addTask() {
      console.log("title: ", this.titleValue);
      console.log("description: ", this.descriptionValue);
      this.tasks.unshift({
        title: this.titleValue,
        description: this.descriptionValue,
        isDone: false,
      });
      console.log(this.tasks);
    },
    deleteTask(task) {
      const index = this.tasks.indexOf(task);
      if (index !== -1) {
        this.tasks.splice(index, 1);
      }
    },
    saveTask() {
      this.addTask();
      this.clearForm();
    },
    cancelTask() {
      this.clearForm();
    },
    clearForm() {
      this.titleValue = "";
      this.descriptionValue = "";
      this.isCreating = false;
    },
  },
};
</script>

<style>
.completed-task {
  text-decoration: line-through;
}
</style>
