<script module>
import { ref } from "vue";

export default {
  setup() {
    const newItem = ref("");
    const tasks = ref([]);

    function storeItem() {
      tasks.value.push({
        id: Date.now(),
        done: false,
        content: newItem.value,
      });
      newItem.value = "";
    }

    function toggleDone(task) {
      task.done = !task.done;
    }

    function delItem(index) {
      tasks.value.splice(index, 1);
    }

    return {
      newItem,
      tasks,
      storeItem,
      toggleDone,
      delItem,
    };
  },
};
</script>

<template>
  <div class="app-container" id="tasklist">
    <h1 class="app-header">Vue TO DO LIST</h1>

    <div class="add-task">
      <input
        type="text"
        autocomplete="off"
        placeholder="Add New Task"
        class="task-input"
        v-model="newItem"
        @keyup.enter="storeItem"
      />
      <input
        type="submit"
        value="."
        class="submit-task"
        title="Add Task"
        @click="storeItem"
      />
    </div>

    <ul class="task-list">
      <li class="task-list-item" v-for="(task, index) in tasks" :key="task.id">
        <label
          class="task-list-item-label"
          :class="{ done: task.done }"
          @click="toggleDone(task)"
        >
          <input type="checkbox" />
          <span>{{ task.content }}</span>
        </label>
        <span class="delete-btn" title="Delete Task" @click="delItem(index)">{{
          task.del
        }}</span>
      </li>
    </ul>
  </div>
</template>
