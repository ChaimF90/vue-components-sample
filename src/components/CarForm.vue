<template>
	<div class='my-well'>
		<input
		name="make"
		v-model="localCar.make" 
		type="text"
		placeholder="Make" 
		class="form-control">

		<input 
		name="model"
		v-model="localCar.model"
		type="text"
		placeholder="Model" 
		class="form-control">

		<input
		v-model="localCar.year" 
		name="year"
		type="text"
		placeholder="Year" 
		class="form-control">

		<button v-on:click="submitClick" class="btn btn-default">Submit</button>
		<button v-on:click="callCancel">cancel</button>
	</div>
</template>

<script>
export default {
	props: ['car'],
	name: 'carform',

	data() {
		var self = this;
		return {
			localCar: Object.assign({}, self.car)
		}
	},

	watch: {
		car(newVal, oldVal) {
			this.localCar = newVal;
		}
	},
	
	methods: {
		submitClick() {
			this.localCar.id = this.car.id;
			this.$emit('addCar', this.localCar)
		},
		callCancel() {
			this.$emit('cancel');
		}
	}
}
</script>

<style>
.my-well{
	margin: auto;
	width: 50%;
	text-align: center;
}	
</style>


