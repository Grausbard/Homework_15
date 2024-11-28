<template>
    <form @submit.prevent="addTask" class="task-form">
      <input v-model="title" placeholder="Заголовок задачи" required class="input-field">
      <textarea v-model="description" placeholder="Описание задачи" required class="input-field"></textarea>
      <button type="submit" class="submit-button">Добавить задачу</button>
    </form>
  </template>
  
  <script>
  export default {
    name: 'TaskForm',
    data() {
      return {
        title: '',
        description: ''
      }
    },
    methods: {
      addTask() {
        if (this.title.trim() && this.description.trim()) {
          this.$emit('add-task', {
            title: this.title,
            description: this.description
          })
          this.title = ''
          this.description = ''
        }
      }
    }
  }
  </script>
  
  <style scoped>
  .task-form {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-bottom: 20px;
  }
  
  .input-field {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 14px;
  }
  
  textarea.input-field {
    min-height: 100px;
    resize: vertical;
  }
  
  .submit-button {
    padding: 10px 15px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
    transition: background-color 0.3s;
  }
  
  .submit-button:hover {
    background-color: #45a049;
  }
  </style>