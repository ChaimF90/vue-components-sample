<template>
	<div>
	<h1>{{localNum}}</h1>
	</div>
</template>

<script>
	export default {
		name: 'test-child',
		props: ['number'],
		data() {
			return {
				localNum: 0
			}
		},
		created() {
			this.localNum = this.number;
		}
	}
</script>