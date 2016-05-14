<template>
 	<div class="item">
 		<div class="content">
 			<i class="icon remove right-float" @click.stop="deleteNote"></i>
 			<a class="header">{{ title }}</a>
 			<div class="desctiption">
 				{{ content }}
 				<a class="ui {{ categoryColor }} tiny label right-float">{{ category }}</a>
 			</div>
 		</div>
 	</div>
</template>

<script>
import store from '../store'
export default {
  props: ['id', 'title', 'content', 'category', 'categoryColor'],
  methods: {
  	deleteNote() {
  		//在这里this指向自身组件
  		store.deleteNote(this.id);
  	}
  }
}
</script>
