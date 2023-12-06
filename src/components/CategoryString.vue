<template>
  <div class="category-string" :class="{'current-category' : (currentCategory == category.id)}" v-if="!editingCategory">
    <a @click="chooseCategory(category)">{{ category.name }}</a>
    <div class="actions" v-if="category.id != '0001'">
      <a class="edit action" @click="editCategory()">✎</a>
      <a class="remove action" @click="deleteCategory(category)">🗑</a>
    </div>
  </div>
  <div class="category-string creating-string" :class="{'current-category' : (currentCategory == category.id)}" v-else>
    <input type="text" autofocus id="categoryName" :value="category.name">
    <div class="actions">
      <a class="edit action" @click="confirmEditingCategory(category)">✓</a>
      <a class="remove action" @click="cancelEditingCategory()">✖</a>
    </div>
  </div>
</template>
  
<script>
  
  export default {
    name: 'CategoryString',
    data() {
      return {
      }
    },
    props: {
      category: {
        type: Object,
        required: true,
      },
    },
    methods: {
      deleteCategory(category){
        this.$store.dispatch('deleteCategory', category.id)
      },
      editCategory(){
        this.$store.dispatch('editCategory')
      },
      chooseCategory(category){
        this.$store.dispatch('chooseCategory', category)
      },
      confirmEditingCategory(category){
        const categoryName = document.getElementById("categoryName").value
        if (categoryName.length > 0){
          this.$store.dispatch('confirmEditingCategory', {
            name: categoryName,
            id: category.id
          })
        }
        else{
          this.cancelEditingCategory();
        }
      },
      cancelEditingCategory(){
        this.$store.dispatch('cancelEditingCategory')
      }
    },
    computed: {
      currentCategory(){
        return this.$store.getters['currentCategory']
      },
      editingCategory(){
        return this.$store.getters['editingCategory']
      },
    },
    created() {
    },
  }
</script>