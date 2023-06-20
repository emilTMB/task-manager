<template>
  <div class="container">
    <h2>Лист задач</h2>
    <div class="add">
      <input type="text" v-model="newTask" placeholder="Добавить новую задачу" />
      <button @click="addTask">Добавить</button>
    </div>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <div class="task" v-if="task.editing">
          <input type="text" v-model="task.title" />
          <button @click="saveTask(task)">Сохранить</button>
        </div>
        <div class="task" v-else>
          {{ task.title }}
          <div class="buttons">
            <button @click="editTask(task)">Изменить</button>
            <button @click="deleteTask(index)">Удалить</button>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';

export default {
  name: 'TaskListPage',
  data() {
    return {
      newTask: ''
    };
  },
  computed: {
    ...mapGetters(['getTasks']),
    tasks() {
      return this.getTasks;
    }
  },
  methods: {
    ...mapActions(['createTask', 'editTask', 'removeTask']),
    addTask() {
      if (this.newTask.trim() !== '') {
        this.createTask({ title: this.newTask, editing: false });
        this.newTask = '';
        this.saveTasksToLocalStorage(); // Сохраняем задачи в localStorage после добавления новой задачи
      }
    },
    editTask(task) {
      task.editing = true;
    },
    saveTask(task) {
      if (task.title.trim() !== '') {
        task.editing = false;
        this.editTask({ index: task.index, task: { ...task } });
        this.saveTasksToLocalStorage(); // Сохраняем задачи в localStorage после сохранения редактированных задач
      }
    },
    deleteTask(index) {
      this.removeTask(index);
      this.saveTasksToLocalStorage(); // Сохраняем задачи в localStorage после удаления задачи
    },
    saveTasksToLocalStorage() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    loadTasksFromLocalStorage() {
      const tasks = localStorage.getItem('tasks');
      if (tasks) {
        this.$store.commit('setTasks', JSON.parse(tasks));
      }
    }
  },
  mounted() {
    this.loadTasksFromLocalStorage(); // Загружаем задачи из localStorage после монтирования компонента
  }
};
</script>