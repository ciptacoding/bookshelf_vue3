<template>
	<div class="mt-8 p-4 md:px-28 lg:px-60 xl:px-72">
		<section class="bg-white shadow-md rounded-md p-4 lg:px-28">
			<header class="mb-4">
				<h1 class="font-bold text-2xl text-center">Bookshelf Vue 3</h1>
			</header>
			<FormInput v-model:input-title="title" v-model:input-author="author" v-model:input-year="year" @submit-form="add"/>
		</section>

		<section class="bg-white shadow-md rounded-md p-4 mt-8">
			<header class="mb-4">
				<h1 class="font-bold text-2xl text-center">List Books</h1>
			</header>
			<div class="mt-4 mb-4 relative overflow-x-auto shadow-md rounded-sm sm:rounded-md">
				<table class="w-full text-sm text-left text-gray-500">
					<thead class="text-xs text-gray-700 uppercase bg-gray-200">
						<tr class="border-b">
							<th scope="col" class="px-6 py-3">No</th>
							<th scope="col" class="px-6 py-3">Title</th>
							<th scope="col" class="px-6 py-3">Author</th>
							<th scope="col" class="px-6 py-3">Year</th>
							<th scope="col" class="px-6 py-3">Actions</th>
						</tr>
					</thead>
					<tbody>
						<tr v-for="(book, index) in books" :key="index" class="bg-white border-b">
							<td class="px-6 py-3">{{ index+1 }}</td>
							<td class="px-6 py-3" v-if="book.isDone">
								<del>{{ book.title }}</del>
							</td>
							<td class="px-6 py-3" v-else>{{book.title}}</td>
							<td class="px-6 py-3">{{ book.author }}</td>
							<td class="px-6 py-3">{{ book.year }}</td>
							<td class="px-6 py-3 flex items-center gap-2">
								<button :title="DeleteTitle" @click="deleteBook(index)" ><Icon icon="material-symbols:delete-outline" height="18" /></button>
								<button :title="UpdateTitle"><Icon icon="mdi:clipboard-edit-outline" height="18" /></button>
								<button :title="DoneTitle" @click="doneRead(index)"><Icon icon="octicon:checklist-24" height="18" /></button>
							</td>
						</tr>
					</tbody>
				</table>
			</div>
		</section>
	</div>
</template>

<script>
	import { Icon } from '@iconify/vue';
	import FormInput from './components/FormInput.vue';
	export default{
		components: {Icon, FormInput},
		data(){
			return{
				// title
				DeleteTitle: 'Delete Book',
				UpdateTitle: 'Update Book',
				DoneTitle: 'Is Done',

				// v-model
				title: '',
				author: '',
				year: '',

				// books storage
				books: []
			}
		},

		methods: {
			add(){
				this.books.unshift({
					title: this.title,
					author: this.author,
					year: this.year,
					isDone: false,
				});
				this.title = ''
				this.author = ''
				this.year = ''
				this.saveToLocalStorage();
			},

			deleteBook(bookIndex){
				this.books = this.books.filter((item, index) => {
					if(index != bookIndex){
						return item;
					}
				});
				this.saveToLocalStorage();
			},

			doneRead(bookIndex){
				this.books = this.books.filter((item, index) => {
					if(index == bookIndex){
						item.isDone = !item.isDone
					}
					return item;
				});
				this.saveToLocalStorage();
			},

			saveToLocalStorage(){
				localStorage.setItem('books', JSON.stringify(this.books))
			},
		},

		mounted(){
			try {
				const storedBooks = localStorage.getItem('books');
				this.books = storedBooks ? JSON.parse(storedBooks) : [];
			} catch (error) {
				console.error('Error retrieving data from local storage:', error);
    			this.books = [];
			}
		}, 
	};
</script>