<template>
	<div id="app">
		<h1>Tarefas</h1>
    <tasks-progress :progress="progress"/>
    <new-task @taskAdded="addTask" />
    <task-grid 
      :tasks="tasks" 
      @taskDeleted="deleteTask" 
      @taskStateChanged="toogleTaskState" />
	</div>
</template>

<script>
import TaskGrid from './components/TaskGrid.vue';
import NewTask from './components/NewTask.vue';
import TasksProgress from './components/TasksProgress.vue';

export default {
  components: {
    TaskGrid,
    NewTask,
    TasksProgress,
  },
  data() {
    return {
      tasks: [
        {
          name: 'lavar a louça', 
          pending: false,
        },
        {
          name: 'Comprar blusa', 
          pending: true,
        },
      ]
    }
  },
  computed: {
    progress() {
      const total = this.tasks.length;
      const done = this.tasks.filter(task => !task.pending).length;

      return Math.round(done / total * 100) || 0;
    }
  },
  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      }
    },
  },
  methods: {
    addTask(task) {
      const sameName = t => t.name === task.name;
      const reallyNew = this.tasks.filter(sameName).length === 0;

      if (reallyNew) {
        this.tasks.push({
          name: task.name,
          pending: task.pending || true,
        })
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    toogleTaskState(index) {
      this.tasks[index].pending = !this.tasks[index].pending;
    }
  },
  created() {
    const tasks = localStorage.getItem('tasks');
    const arrayFromStorage = JSON.parse(tasks);
    this.tasks = Array.isArray(arrayFromStorage) 
      ? arrayFromStorage 
      : [];
  },
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>
