<template>
    <div class="task" :class="{ 'completed': task.completed }">
      <div class="task-content">
        <h3>{{ task.title }}</h3>
        <p>{{ task.description }}</p>
      </div>
      <div class="task-actions">
        <input type="checkbox" :checked="task.completed" @change="toggleCompleted" class="checkbox">
        <button @click="showDetails" class="button details-button">Подробнее</button>
        <button @click="deleteTask" class="button delete-button">Удалить</button>
      </div>
      <teleport to="body">
        <div v-if="showModal" class="modal">
          <div class="modal-content">
            <h2>{{ task.title }}</h2>
            <p>{{ task.description }}</p>
            <slot></slot>
            <button @click="showModal = false" class="button close-button">Закрыть</button>
          </div>
        </div>
      </teleport>
    </div>
  </template>
  
  <script>
  export default {
    name: 'TaskItem',
    props: ['task'],
    data() {
      return {
        showModal: false
      }
    },
    methods: {
      toggleCompleted() {
        this.$emit('toggle-completed', this.task.id)
      },
      deleteTask() {
        this.$emit('delete-task', this.task.id)
      },
      showDetails() {
        this.showModal = true
      }
    }
  }
  </script>
  
  <style scoped>
  .task {
    border: 1px solid #ddd;
    padding: 15px;
    margin-bottom: 15px;
    background-color: #fff;
    border-radius: 4px;
    transition: background-color 0.3s;
  }
  
  .task.completed {
    background-color: #e8f5e9;
  }
  
  .task-content h3 {
    margin: 0 0 10px 0;
    color: #333;
  }
  
  .task-content p {
    margin: 0;
    color: #666;
  }
  
  .task-actions {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    margin-top: 10px;
  }
  
  .checkbox {
    margin-right: 10px;
  }
  
  .button {
    padding: 5px 10px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 14px;
    transition: background-color 0.3s;
  }
  
  .details-button {
    background-color: #2196F3;
    color: white;
    margin-right: 5px;
  }
  
  .delete-button {
    background-color: #f44336;
    color: white;
  }
  
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .modal-content {
    background-color: white;
    padding: 20px;
    border-radius: 4px;
    max-width: 500px;
    width: 100%;
  }
  
  .close-button {
    background-color: #ccc;
    color: #333;
    margin-top: 10px;
  }
  </style>