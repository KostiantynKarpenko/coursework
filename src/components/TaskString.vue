<template>
  <div class="task-string" v-if="!editingTask">
    <div class="task-n-check">
      <!-- <input type="checkbox" v-bind:on-change="completeTask(task)"> -->
      <a>{{ task.name }}</a>
    </div>
    <div class="actions">
      <a class="edit action" @click="editTask()">✎</a>
      <a class="remove action" @click="deleteTask(task)">🗑</a>
    </div>
  </div>
  <div class="task-string creating-string" v-else>
    <input type="text" autofocus id="taskName" :value="task.name">
    <div class="actions">
      <select id="taskCategory">
        <option v-for="category in categories" 
        :key="category.id" 
        :value="category.id" 
        :selected="category.id === task.category">{{ category.name }}</option>
      </select>
      <a class="confirm action" @click="confirmEditingTask(task)">✓</a>
      <a class="cancel action" @click="cancelEditingTask()">✖</a>
    </div>
  </div>
</template>
    
  <script>
    
    export default {
      name: 'TaskString',
      data() {
        return {
        }
      },
      props: {
        task: {
          type: Object,
          required: true,
        },
      },
      methods: {
        deleteTask(task){
          this.$store.dispatch('deleteTask', task)
        },
        editTask(){
          this.$store.dispatch('editTask')
        },
        completeTask(task){
          this.$store.dispatch('completeTask', task)
        },
        confirmEditingTask(task){
          const taskName = document.getElementById("taskName").value
          const taskCategory = document.getElementById("taskCategory").value
          if (taskName.length > 0){
          this.$store.dispatch('confirmEditingTask', {
            name: taskName,
            id: task.id,
            category: taskCategory,
            dateCreated: task.dateCreated,
            dateCompleted: task.dateCompleted
        })
      }
      else{
        this.cancelEditingTask();
      }
        },
        cancelEditingTask(task){
          this.$store.dispatch('cancelEditingTask', task)
        }
      },
      computed: {
        editingTask(){
          return this.$store.getters['editingTask'];
        },
        categories(){
          return this.$store.getters['getCategories']
        }
      },
      created() {
      },
    }
  </script>