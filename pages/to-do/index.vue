<template>
  <div class="flex justify-end mt-10 mb-3" v-if="!showFormCreateTask">
    <button
      @click="onCancelForm"
      type="button"
      class="rounded-full bg-blue-500 px-5 py-3 font-semibold text-white"
    >
      Add New Task
    </button>
  </div>
  <div class="mt-10 mb-8" v-else>
    <FormCreateTask @create-task="onCreateTask" @cancel-form="onCancelForm" />
  </div>

  <!-- To Do List Table-->
  <ToDoList
    :name="namePerson"
    :tasks="tasks"
    :numberOfTasks="tasks.length"
    @mark-task-completed="markTaskCompleted"
    @delete-task="deleteTask"
  />
</template>

<script>
export default {
  data() {
    return {
      namePerson: "John Doe",
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
    onCreateTask(newTask) {
      this.tasks.unshift({
        name: newTask.name,
        description: newTask.description,
        status: false,
      });
      this.showFormCreateTask = !this.showFormCreateTask;
    },
    onCancelForm() {
      this.showFormCreateTask = !this.showFormCreateTask;
    },
    markTaskCompleted(index) {
      this.tasks[index].status = !this.tasks[index].status;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>
