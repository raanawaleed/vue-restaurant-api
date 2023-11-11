<template>
  <div>
    <h2>Dish List</h2>
    <ul>
      <li v-for="dish in dishes" :key="dish.id">
        <img :src="dish.image" alt="Dish Image" />
        <h3>{{ dish.name }}</h3>
        <p>{{ dish.description }}</p>
        <p>Price: ${{ dish.price }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      dishes: [] // Initialize an empty array to store the list of dishes
    };
  },
  methods: {
    // Implement a method to fetch the list of dishes from your Laravel API
    async fetchDishes() {
    try {
      const response = await axios.get('http://127.0.0.1:8000/api/dishes');

      // Update the dishes data property with the fetched list of dishes
      this.dishes = response.data;
    } catch (error) {
      console.error('Request error:', error);
      // Handle any request error
    }
  }
  },
  created() {
    // Call the method to fetch dishes when the component is created
    this.fetchDishes();
  }
};
</script>
