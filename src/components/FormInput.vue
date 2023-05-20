<template>
	<div>
		<header class="mb-4">
				<h1 class="font-bold text-2xl text-center">Bookshelf Vue 3</h1>
		</header>
	  <div class="mb-4">
		 <label for="addTitle" class="block mb-1">Title</label>
		 <input @input="$emit('update:input-title', $event.target.value)" :value="inputTitle" type="text" 
			id="addTitle" class="rounded-md border-black w-full bg-gray-100 border border-solid py-1 px-2 focus:outline-cyan-500" placeholder="Input title">
	  </div>
	  <div class="mb-4">
		 <label for="addAuthor" class="block mb-1">Author</label>
		 <input @input="$emit('update:input-author', $event.target.value)" :value="inputAuthor" type="text" 
			id="addAuthor" class="rounded-md border-black w-full bg-gray-100 border border-solid py-1 px-2 focus:outline-cyan-500" placeholder="Input author">
	  </div>
	  <div class="mb-8">
		 <label for="addYear" class="block mb-1">Year</label>
		 <input @input="$emit('update:input-year', $event.target.value)" :value="inputYear" type="text" 
			id="addYear" class="rounded-md border-black w-full bg-gray-100 border border-solid py-1 px-2 focus:outline-cyan-500" placeholder="Input year">
	  </div>
	  <div class="flex justify-end">
		 <button @click="add" class="bg-blue-500 px-8 py-1 text-white rounded-md shadow-md mb-4">Add Book</button>
	  </div>
	</div>
 </template>
 
 <script>
 export default {
	props: {
	  inputTitle: String,
	  inputAuthor: String,
	  inputYear: String,
	},
	emits: ['update:input-title', 'update:input-author', 'update:input-year'],
	methods: {
	  add() {
		 this.$emit('submit-form');
	  },
	},
 };
 </script>
 