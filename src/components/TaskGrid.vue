<template>
  <div class="task-grid">
    <template>
      <div v-for="task in tasks" :key="task.name">
        <task-comp :task="task" />
      </div>
    </template>
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
