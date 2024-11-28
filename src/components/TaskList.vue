<template>
    <div class="task-list">
      <h2>Список задач</h2>
      <div class="task-stats">
        <p>Всего задач: {{ totalTasks }}</p>
        <p>Выполнено задач: {{ completedTasks }}</p>
      </div>
      <TaskForm @add-task="addTask" />
      <div class="tasks-container">
        <TaskItem
          v-for="task in tasks"
          :key="task.id"
          :task="task"
          @delete-task="deleteTask"
          @toggle-completed="toggleCompleted"
        />
      </div>
    </div>
  </template>
  
  <script>
  import TaskItem from './TaskItem.vue'
  import TaskForm from './TaskForm.vue'
  
  export default {
    name: 'TaskList',
    components: {
      TaskItem,
      TaskForm
    },
    data() {
      return {
        tasks: []
      }
    },
    computed: {
      totalTasks() {
        return this.tasks.length
      },
      completedTasks() {
        return this.tasks.filter(task => task.completed).length
      }
    },
    methods: {
      addTask(newTask) {
        this.tasks.push({
          id: Date.now(),
          title: newTask.title,
          description: newTask.description,
          completed: false
        })
      },
      deleteTask(taskId) {
        this.tasks = this.tasks.filter(task => task.id !== taskId)
      },
      toggleCompleted(taskId) {
        const task = this.tasks.find(task => task.id === taskId)
        if (task) {
          task.completed = !task.completed
        }
      }
    }
  }
  </script>
  
  <style scoped>
  .task-list {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    background-color: #f5f5f5;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  h2 {
    color: #333;
    margin-bottom: 20px;
  }
  
  .task-stats {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
    font-size: 14px;
    color: #666;
  }
  
  .tasks-container {
    margin-top: 20px;
  }
  </style>