<template>
  <div class="table-container">
  <table class="table table-striped table-hover">
    <thead>
      <th>Make</th>
      <th>Model</th>
      <th>Year</th>
      <th>Actions</th>
    </thead>
    <tbody>
      <tr v-for="car in cars">
        <td>{{car.make}}</td>
        <td>{{car.model}}</td>
        <td>{{car.year}}</td>
        <td>
          <button 
          v-on:click="callDelete(car.id)" 
          class="btn btn-danger">Delete</button>

          <button 
          v-on:click="callEdit(car)" 
          class="btn btn-warning">Edit</button>
        </td>
      </tr>
    </tbody>
  </table>
  </div>
</template>

<script>
export default {
  name: 'child',
  props: ['cars'],
  methods: {
    handleBlur(e) {
      this.$emit('changeText', e.target.value);
    },
    callDelete(id) {
      this.$emit('delete', id);
    },
    callEdit(car) {
      this.$emit('edit', car);
    }
  }
}
</script>

<style>
  .table-container{
    margin-top: 40px;
  }
</style>






