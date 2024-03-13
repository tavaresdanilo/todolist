<script>
export default {
  name: "App",
  data() {
    return {
      tasks: [],
      textInput: "",
      isCompleted: false,
    };
  },
  methods: {
    createTask() {
      if (!this.textInput || this.textInput.trim() === "") {
        return;
      } else {
        this.tasks.push({
          textInput: this.textInput,
        }),
          (this.showCheckboxInput = true);
        this.showDeleteButton = true;
        this.textInput = "";
      }
    },
    taskCompleted(index) {
      this.tasks[index].isCompleted = !this.tasks[index].isCompleted;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>

<template>
  <div
    class="h-screen flex flex-col justify-center items-center bg-[hsl(35,73,95)]"
  >
    <h1
      class="text-3xl w-full font-bold text-zinc-600 text-center fixed top-0 p-4 bg-[hsl(35,73,95)]/80 backdrop-blur-sm"
    >
      Tarefas
    </h1>
    <div
      class="flex flex-row justify-center items-center bg-[hsl(35,73,95)]/80 backdrop-blur-sm fixed bottom-0 gap-4 w-full h-[10vh] border-inherit border-2 border-zinc-600"
    >
      <input
        type="text"
        placeholder="Escreva a sua tarefa"
        v-model="textInput"
        class="p-2 rounded-lg w-[70vw] outline-none text-xl font-semibold border-2 border-zinc-600"
      />
      <span
        @click.prevent="createTask()"
        class="material-symbols-outlined cursor-pointer text-3xl text-zinc-600"
      >
        library_add
      </span>
    </div>
    <div class="">
      <ul v-for="(task, index) in tasks" class="">
        <li
          class="flex justify-between items-center bg-zinc-300 p-2 rounded-lg w-[80vw] m-2"
        >
          <p
            v-if="task.isCompleted"
            class="text-2xl font-semibold line-through text-emerald-600"
          >
            {{ task.textInput }}
          </p>
          <p v-else class="text-2xl font-semibold text-zinc-600">
            {{ task.textInput }}
          </p>
          <div class="flex flex-row gap-2">
            <span
              v-if="task.isCompleted"
              @click.prevent="taskCompleted(index)"
              class="material-symbols-outlined cursor-pointer text-emerald-600"
              >check_box
            </span>
            <span
              v-else
              @click.prevent="taskCompleted(index)"
              class="material-symbols-outlined material-symbols-outlined cursor-pointer text-zinc-600"
              >check_box_outline_blank</span
            >
            <span
              @click.prevent="deleteTask(index)"
              class="material-symbols-outlined cursor-pointer text-rose-600"
              >delete</span
            >
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>
