<template>
	<div>
		<button v-on:click='buttonClick'>Click me</button>
		<test-child :number="val"></test-child>
	</div>
</template>

<script>
	import child from './testChild';
	export default {
		name: 'test',
		components: {
			'test-child': child
		},
		data() {
			return {
				val: 0
			}
		},

		methods: {
			buttonClick() {
				this.val++;
			}
		}

	}
</script>