<style>
#categories {
  background-color: #3E3E40;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  width: 300px;
  height: 100%;
  overflow: hidden;
  color: #8F9497;
}

#categories div.list {
  margin-left: 30px;
  font-family: 'Raleway', sans-serif;
}

#categories .item {
  padding-bottom: 7px !important;
}

#categories h2 {
  margin-top: 20px;
  margin-left: 15px;
  font-family: 'Raleway', sans-serif;
  font-weight: 400;
  font-size: 14px;
  text-transform: uppercase;
}

#categories button {
  position: absolute;
  bottom: 15px;
  right: 15px;
}

#cat-header {
  background-color: #4A5557;
  height: 60px;
  position: relative;
}

#cat-header h2 {
  font-family: 'Raleway', sans-serif !important;
  font-weight: 300;
  font-size: 20px;
  text-transform: uppercase;
  position: absolute;
  bottom: 10px;
  left: 15px;
}

#categories h2 .bookmark.icon,
#categories h2 .add.icon {
  color: #87568D;
}

.right-float {
  float: right;
}

.selected {
  color: #87568D;
}

.clickable {
  opacity: 1;
  -webkit-transition: opacity .25s ease-in-out;
  transition: opacity .25s ease-in-out;
}

.container {
  margin: 15px;
}

.container .item span {
	color: #9E9E9F;
}

.container .item i {
	color: #ffffff;
}
i.remove.icon {
  opacity: 0;
  -webkit-transition: opacity .25s ease-in-out;
  transition: opacity .25s ease-in-out;
}

i.write.icon {
  opacity: 0;
  -webkit-transition: opacity .25s ease-in-out;
  transition: opacity .25s ease-in-out;
}

div.content:hover i.write.icon {
  opacity: 1;
}

div.content:hover i.remove.icon {
  opacity: 1;
}
</style>
<template>
	<div>
		<div id="categories">
			<div id="cat-header">
				<h2><i class="bookmark icon"></i>NOTE</h2>
			</div>
			<div class="container">
				<h2>标签
					<span class="clickable right-float">
						<i class="add icon" @click="addCategory" title="添加标签"></i>
					</span>
				</h2>
				<div class="ui list">
					<div class="item clickable">
						<div class="content">
							<a class="ui grey empty circular label">
							</a>
							<span @click="categorySelected('')">All</span>
						</div>
					</div>
					<div class="item clickable" v-for="(name, color) in categories">
						<div class="content">
							<a class="ui {{ color }} empty circular label"></a>
							<span @click="categorySelected(name)" :class="{selected: selectedCategory === name}">
								{{ name }}
							</span>

							<i class="remove icon right-float" @click="deleteCategory(name)" title="删除"></i>
							<i class="write icon right-float" @click="editCategory(name, color)" title="编辑"></i>
						</div>
					</div>
				</div>
				<button class="ui grey inverted basic icon circular button right-float" @click="addNode" title="添加内容"><i class="icon add"></i></button>
			</div>
		</div>
		<category-modal></category-modal>
		<edit-category-modal :category_name="category_name"></edit-category-modal>
		<note-modal :note_modal_id="note_modal_id" :categories="categories"></note-modal>
</template>

<script>
import store from '../store'
import categoryModal from './categoryModal.vue'
import noteModal from './editNoteModal.vue'
import editCategoryModal from './editCategoryModal.vue'

export default {
  data () {
  	return {
  		selectedCategory: '',
  		note_modal_id: 'add_note',
  		category_name: '' 
  	}
  },
  props: ['categories'],
  components: {
  	categoryModal,
  	editCategoryModal,
  	noteModal
  },
  methods: {
  	categorySelected(category) {
  		this.selectedCategory = category;
  		//$dispatch实现事件在组件间的通信
  		this.$dispatch('category-selected', category);
  	},
  	deleteCategory(category) {
  		store.deleteCategory(category);
  	},
  	editCategory(name, color) {
  		this.category_name = name;
  		this.$broadcast('edit-category', name, color);
  	},
  	addCategory() {
  		this.$broadcast('add-category');
  	},
  	addNode() {
  		this.$broadcast('add-note');
  	}
  }
}
</script>
