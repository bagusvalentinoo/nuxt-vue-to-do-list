<template>
  <div class="flex justify-end mt-10 mb-3" v-if="!showFormCreateTask">
    <button
      @click="toggleFormCreateTask"
      type="button"
      class="rounded-full bg-blue-500 px-5 py-3 font-semibold text-white"
    >
      Add New Task
    </button>
  </div>
  <div class="mt-10 mb-8" v-else>
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
          @click="toggleFormCreateTask"
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
  </div>
  <div class="relative overflow-x-auto">
    <table class="w-full text-sm text-left">
      <thead class="uppercase bg-gray-700 text-gray-400 text-center text-base">
        <tr>
          <th scope="col" class="w-8 px-6 py-3"></th>
          <th scope="col" class="w-10 px-6 py-3">No</th>
          <th scope="col" class="px-6 py-3">Name</th>
          <th scope="col" class="px-6 py-3">Description</th>
          <th scope="col" class="px-6 py-3">Status</th>
          <th scope="col" class="px-6 py-3">Action</th>
        </tr>
      </thead>
      <tbody class="text-base">
        <tr
          class="border-b bg-gray-800 text-white"
          v-for="(task, index) in tasks"
          :key="index"
          :class="{ 'line-through': task.status }"
        >
          <td
            scope="row"
            class="px-6 py-4 font-medium whitespace-nowrap text-white text-center"
          >
            <input
              type="checkbox"
              :checked="task.status"
              @change="markTaskCompleted(index)"
            />
          </td>
          <td
            scope="row"
            class="px-6 py-4 font-medium whitespace-nowrap text-white text-center"
          >
            {{ index + 1 }}
          </td>
          <td class="px-6 py-4">{{ task.name }}</td>
          <td class="px-6 py-4">{{ task.description }}</td>
          <td class="px-6 py-4 text-center">
            {{ task.status ? "Completed" : "Not Completed" }}
          </td>
          <td class="px-6 py-4 text-center">
            <button
              type="button"
              class="rounded-full bg-red-700 px-5 py-3 font-semibold text-white"
              @click="deleteTask(index)"
            >
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nameTask: "",
      descriptionTask: "",
      showFormCreateTask: false,
      tasks: [
        {
          name: "Task 1",
          description:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Mollitia, a!",
          status: false, // true = completed, false = not completed
        },
        {
          name: "Task 2",
          description:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Mollitia, a!",
          status: false,
        },
        {
          name: "Task 3",
          description:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Mollitia, a!",
          status: false,
        },
      ],
    };
  },
  methods: {
    createNewTask() {
      if (this.nameTask && this.descriptionTask) {
        this.tasks.unshift({
          name: this.nameTask,
          description: this.descriptionTask,
          status: false,
        });
        this.nameTask = "";
        this.descriptionTask = "";
        this.showFormCreateTask = false;
      } else {
        alert("Please fill in all fields!");
      }
    },
    markTaskCompleted(index) {
      this.tasks[index].status = !this.tasks[index].status;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleFormCreateTask() {
      this.showFormCreateTask = !this.showFormCreateTask;
    },
  },
};
</script>
