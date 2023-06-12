<template>
  <form @submit.prevent="createNewTask">
    <div class="flex flex-col mb-2">
      <label for="name" class="mb-2">Name</label>
      <input
        type="text"
        name="name"
        id="name"
        class="rounded-lg border-gray-300 border-2 p-2"
        placeholder="Insert new task name here"
        v-model="nameTask"
      />
    </div>
    <div class="flex flex-col mb-2">
      <label for="description" class="mb-2">Description</label>
      <textarea
        name="description"
        id="description"
        class="rounded-lg border-gray-300 border-2 p-2"
        placeholder="Insert new task description here"
        v-model="descriptionTask"
      ></textarea>
    </div>
    <div class="flex justify-end mt-5">
      <button
        type="button"
        class="rounded-full bg-gray-500 px-5 py-3 font-semibold text-white mr-2"
        @click="cancelForm"
      >
        Cancel
      </button>
      <button
        type="submit"
        class="rounded-full bg-green-500 px-5 py-3 font-semibold text-white"
      >
        Save
      </button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      nameTask: "",
      descriptionTask: "",
    };
  },
  methods: {
    createNewTask() {
      if (this.nameTask && this.descriptionTask) {
        this.$emit("create-task", {
          name: this.nameTask,
          description: this.descriptionTask,
        });
        this.nameTask = "";
        this.descriptionTask = "";
      } else {
        alert("Please fill in all fields!");
      }
    },
    cancelForm() {
      this.$emit("cancel-form");
    },
  },
};
</script>