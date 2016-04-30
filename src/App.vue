<template>
  <div id="app">
    <side-bar :categories="categories" v-on:category-selected="setSelectedCategory"></side-bar>
    <note-list :notes="notes | filterByCategory selectedCategory" :categories="categories"></note-list>
  </div>
</template>

<script>
import store from './store'
import { filterByCategory } from './filters'
import sideBar from './components/sideBar.vue'
import noteList from './components/noteList.vue'


export default {
  data () {
    return {
      categories: {},
      notes: {},
      selectedCategory: ''
    }
  },
  components: {
    sideBar,
    noteList
  },
  filters: {
    filterByCategory
  },
  created() {
    store.on('data-updated', this.updateListings)
  },
  methods: {
    updateListings (categories, notes) {
      this.categories = categories;
      this.notes = notes;
    },
    setSelectedCategory (category) {
      this.selectedCategory = category;
    }
  }
}
</script>
