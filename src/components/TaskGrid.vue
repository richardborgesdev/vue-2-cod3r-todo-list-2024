<template>
  <div class="task-grid">
    <template v-if="tasks.length">
      <div v-for="task in tasks" :key="task.name">
        <task-comp :task="task" />
      </div>
    </template>
    <p class="no-task" v-else>
      Sua vida está em dia :)
    </p>
  </div>
</template>

<script>
import TaskComp from './TaskComp.vue';

export default {
  components: {
    TaskComp,
  },
  props: {
    tasks: {
      type: Array,
      required: true,
    }
  }
}
</script>

<style>
.task-grid {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.task-grid .task {
  margin: 10px;
}

.no-task {
  color: #AAA;
  font-size: 1.7rem;;
}
</style>
