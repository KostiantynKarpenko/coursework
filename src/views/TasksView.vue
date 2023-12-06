<template>
  <div class="categories-and-tasks">
    <CategoriesTab/>
    <TasksTab/>
    <button class="sign-out" @click="signOut()">Sign out</button>
  </div>
</template>

<script>

import CategoriesTab from '@/components/CategoriesTab.vue'
import TasksTab from '@/components/TasksTab.vue'
import router from '@/router'

export default {
  name: 'TasksView',
  components: {
    CategoriesTab,
    TasksTab
  },
  methods: {
    signOut(){
      this.$store.dispatch('signOut')
      router.push('/')
    }
  }
}
</script>
