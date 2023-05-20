<template>
	<div class="mt-8 p-4 md:px-28 lg:px-60 xl:px-72">
		<section class="bg-white shadow-md rounded-md p-4 lg:px-28">
			<FormInput v-model:input-title="title" v-model:input-author="author" v-model:input-year="year" @submit-form="add"/>
		</section>

		<section class="bg-white shadow-md rounded-md p-4 mt-8">
			<ListBooks :books="books" @delete-book="deleteBook" @done-read="doneRead"/>
		</section>
	</div>
</template>

<script>
	import FormInput from './components/FormInput.vue';
	import ListBooks from './components/ListBooks.vue';
	export default{
		components: {FormInput, ListBooks},
		data(){
			return{
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