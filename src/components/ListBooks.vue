<template>
	<div>
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
							<button :title="DoneTitle" @click="doneRead(index)"><Icon icon="octicon:checklist-24" height="18" /></button>
							<button :title="DeleteTitle" @click="deleteBook(index)">
								<Icon icon="material-symbols:delete-outline" height="18" />
							</button>
						</td>
					</tr>
				</tbody>
			</table>
		</div>
	</div>
</template>

<script>
	import { Icon } from '@iconify/vue';

	export default{
		components: {Icon},
		data(){
			return {
				// title
				DeleteTitle: 'Delete Book',
				DoneTitle: 'Is Done',
			}
		},
		props: {
			books: {
				type: Array,
				default: [],
			}
		},
		methods: {
			deleteBook(index){
				this.$emit('delete-book', index)
			},
			updateBook(index){
				this.$emit('update-book', index)
			},
			doneRead(index){
				this.$emit('done-read', index)
			}
		}
	}
</script>
