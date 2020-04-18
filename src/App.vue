<template>
  <div id="app">
    <h1>TO-DO LIST</h1>
    <TaskProgress :progress="progress" />
    <NewTask @taskAdded="addTask" @deleteAll="deleteAllTasks" />
    <TaskGrid 
    @taskDeleted="deleteTask" 
    @taskStateChanged="toggleTaskState"
    :tasks="tasks" />
  </div>
</template>

<script>
import TaskProgress from "./components/TaskProgress";
import NewTask from "./components/NewTask.vue";
import TaskGrid from "./components/TaskGrid.vue";

export default {
  components: { NewTask, TaskGrid, TaskProgress },
  data() {
    return {
      tasks: []
    };
  },
  methods: {
    addTask(task) {
      const sameName = t => t.name === task.name;
      const reallyNew = this.tasks.filter(sameName).length == 0;

      let nameTruncated = task.name.substring(0, 163);
      nameTruncated = nameTruncated.length < 163 ? nameTruncated+'' : nameTruncated+'...';

      reallyNew && task.name.length && this.tasks.push({
          name: nameTruncated,
          pending: task.pending || true
        });
    },
    deleteTask(i){
      this.tasks.splice(i, 1);
    },
    deleteAllTasks(){
      if(this.tasks.length > 0 && confirm('Deseja realmente apagar todas as tarefas?')){
        this.tasks = [];
      }
    },
    toggleTaskState(i){
      this.tasks[i].pending = !this.tasks[i].pending;
    }
  },
  computed: {
    progress() {
      const total = this.tasks.length;
      const done = this.tasks.filter(t => !t.pending).length;
      return Math.round( done / total * 100) || 0;
    }
  },
  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      }
    }
  },
  created() {
    const json = localStorage.getItem('tasks');
    this.tasks = JSON.parse(json) || [];
  }
  
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;
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
  font-weight: bold;
  font-size: 3rem;
}

</style>
