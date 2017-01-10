<template>
  <div class="container">
  <button v-on:click="toggleForm" class="btn btn-primary my-button">Add Car</button> 
  <child
  v-on:edit="editCar" 
  v-on:delete="deleteCar" 
  :cars="cars"></child>
  <carform
  v-on:cancel="cancel"
  :car="car" 
  v-if="showForm"
  v-on:addCar="addNewCar"></carform>
  </div>
</template>

<script>
import Child from './components/Child'
import Carform from './components/CarForm';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Child,
    Carform
  },
  created() {
    this.getAllCars();
  },
  data() {
    return {
      cars: [],
      car:{make: '', model:'', year: ''},
      showForm: false,
      editMode: false
    }
  },
  methods: {
    handleChange(value) {
      this.text = value;
    },
    addNewCar(newCar) {
      if(!this.editMode) {
        axios.post('http://localhost:3000/api/cars/add', newCar)
        .then(results => {
          this.cars.push(results.data[0]);
          this.showForm = false;
        })
      } else {
        axios.post('http://localhost:3000/api/cars/editCar', newCar)
        .then(results => {
          this.getAllCars();
          this.showForm = false;
          this.editMode = false;
        })
      }
    },
    toggleForm() {
      this.showForm = true;
    },
    deleteCar(id) {
      axios.post('http://localhost:3000/api/cars/deleteCar', {id})
      .then(results => {
        if(results.data) {
          this.getAllCars();
        }
      })
    },
    getAllCars() {
      axios.get('http://localhost:3000/api/cars/getAllCars').then(results => {
        this.cars = results.data;
      })
    },
    editCar(car) {
      this.car = car;
      this.showForm = true;
      this.editMode = true;
    },
    cancel() {
      this.showForm = false;
    }
  }
}
</script>

<style>
.my-button{
  margin-top: 20px;
}
</style>
