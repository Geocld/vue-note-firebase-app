<template>
<div>
	<div id="links-container">
		<div id="toolbar">
			<div class="ui inverted icon fluid input">
				<input v-model="query" type="text" placeholder="过滤关键字">
				<i class="search icon"></i>
			</div>
		</div>
		<div class="ui relaxed divided selection list">
			<note-item v-for="note in note_arr | filterBytitle query"
				:id="note.id"
				:title="note.title"
				:content="note.content"
				:category="note.category"
				:category-color="categories[note.category]"
				@click="edit_note(id, note)">
			</note-item>
		</div>
	</div>
	<edit-note-modal :content_id="content_id" :note_modal_id="note_modal_id" :categories="categories"></edit-note-modal>
</div>
</template>

<script>
import noteItem from './noteItem.vue'
import editNoteModal from './editNoteModal.vue'
import { filterBytitle} from '../filters'
export default {
	props: ['notes', 'categories'],
	data() {
		return {
			query: '',
			note_modal_id: 'edit_note',
			content_id: ''
		}
	},
	computed: {
		note_arr() {
			var arr = [];
			for (var i in this.notes) {
				if (this.notes.hasOwnProperty(i)) {
					this.notes[i].id = i;
					arr.push(this.notes[i]);
				}
			}
			arr.sort(function(a, b) {
				return new Date(b.date.replace(/\s/ig,'T')) - new Date(a.date.replace(/\s/ig,'T'));
			});
			return arr;
		}
	},
 	components: {
 		noteItem,
 		editNoteModal
 	},
 	filters: {
 		filterBytitle
 	},
 	methods: {
 		edit_note(id, note) {
 			//将当前note的id复制到content_id中，传到子组件弹窗
 			this.content_id = id;
 			//note的内容在弹窗打开时即使用，也就是在events中使用，直接传值即可
 			this.$broadcast('edit-note',note);
 		}
 	}
}
</script>
