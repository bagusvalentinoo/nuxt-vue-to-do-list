<template>
  <div class="relative overflow-x-auto">
    <h1 class="font-bold text-3xl text-purple-700 my-4">
      Ini tugas punya {{ name }}
    </h1>
    <h3 class="font-bold text-xl text-purple-900 my-2">
      Jumlah tugas ada :
      <span class="text-red-500">{{ numberOfTasks }}</span>
    </h3>
    <h3 class="font-bold text-xl text-purple-900 my-2">
      Yang sudah selesai :
      <span class="text-red-500">{{ numberOfCompletedTasks }}</span>
    </h3>
    <h3 class="font-bold text-xl text-purple-900 my-2">
      Yang belum selesai :
      <span class="text-red-500">{{ numberOfUncompletedTasks }}</span>
    </h3>
    <table class="w-full text-sm text-left mt-3">
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
        <tr v-if="tasks.length === 0">
          <td
            colspan="6"
            class="border-b bg-gray-800 text-white text-center py-3"
          >
            Tidak ada data tugas
          </td>
        </tr>
        <tr
          class="border-b bg-gray-800 text-white"
          v-for="(task, index) in tasks"
          :key="index"
          :class="{ 'line-through': task.status }"
          v-else
        >
          <td
            scope="row"
            class="px-6 py-4 font-medium whitespace-nowrap text-white text-center"
          >
            <input
              type="checkbox"
              :checked="task.status"
              @change="$emit('markTaskCompleted', index)"
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
              @click="$emit('deleteTask', index)"
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
  props: {
    name: {
      type: String,
    },
    numberOfTasks: {
      type: Number,
    },
    tasks: {
      type: Array,
    },
  },
  computed: {
    numberOfCompletedTasks() {
      return this.tasks.filter((task) => task.status).length;
    },
    numberOfUncompletedTasks() {
      return this.tasks.filter((task) => !task.status).length;
    },
  },
};
</script>
