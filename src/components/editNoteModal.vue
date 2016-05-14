<template>
  <div id="{{ note_modal_id }}" class="ui small modal">
  	<i class="close icon"></i>
  	<div class="header">
  		{{ header_name }}
  	</div>
  	<div class="content">
  		<form class="ui form">
  			<div class="field">
  				<label>标题</label>
  				<input type="text" placeholder="请输入标题" v-model="title">
  			</div>
  			<div class="field">
  				<label>正文内容</label>
  				
          <textarea cols="30" rows="10" placeholder="请输入内容" v-model="content"></textarea>
  			</div>
  			<div class="field">
  				<label>分类</label>
  				<select class="ui simple dropdown" v-model="noteCategory">
  					<option value="">请选择</option>
  					<option v-for="(name, color) in categories" value="{{name}}">{{name}}</option>
  				</select>
  			</div>
  		</form>
  	</div>
  	<div v-if="note_modal_id=='add_note'" class="actions">
  		<div @click="addNote" class="ui inverted purple button">添加</div>
  	</div>
  	<div v-if="note_modal_id=='edit_note'" class="actions">
  		<div @click="editNote" class="ui inverted purple button">编辑</div>
  	</div>
  </div>
</template>

<script>
import moment from 'moment'
import store from '../store'

export default {
  props: ['categories', 'note_modal_id', 'content_id'],
  data() {
  	return {
  		title: '',
  		content: '',
  		noteCategory: '',
  		header_name: ''
  	}
  },
  methods: {
  	addNote() {
  		if(this.title === '' || this.content === '' || this.noteCategory === '') {
  			return false;
  		}
      var now = moment().format('YYYY-MM-DD HH:mm');
  		const newNote = {
  			title: this.title,
  			content: this.content,
  			category: this.noteCategory,
        date: now
  		};
  		store.addNote(newNote);
  		$('#add_note').modal('hide');
  	},
  	editNote() {
      if(this.title === '' || this.content === '' || this.noteCategory === '') {
        return false;
      }
      var now = moment().format('YYYY-MM-DD HH:mm');
  		const editContent = {
  			title: this.title,
  			content: this.content,
  			category: this.noteCategory,
        date: now
  		};
  		store.editNote(this.content_id, editContent);
  		$('#edit_note').modal('hide');
  	}
  },
  events: {
  	'add-note': function() {
  		this.title = this.content = this.noteCategory = '';
  		this.header_name = '添加内容';
  		$('#add_note').modal('show');
  	},
  	'edit-note': function(note) {
  		this.title = note.title;
  		this.content = note.content;
  		this.noteCategory = note.category;
      //console.log(note.title)
  		this.header_name = '编辑内容';
  		$('#edit_note').modal('show');
  	}
  }
}
</script>
