<template>
	<ul class="pagination justify-content-center">
   	<li v-for="i of Math.ceil(count / maxElem)" :key="i" @click="changePage(i)" 
			v-bind:class="[{active: i === page}, 'page-item']">
			<a class="page-link ml-3" href="#">{{i}}</a>
		</li>
	</ul>
</template>

<script>
export default {
	props: ['count', 'page', 'maxElem'],
	methods: {
		changePage(page) {
			this.$emit('change-page', page)
		}
	}
}
</script>
