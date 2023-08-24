<template>
  <h1>{{ name }}</h1>
  <input type="text" v-model="name">
  <button @click="placeOrder">Place Order</button>
  <button @click="removeWatcher">Hide cart alert</button>
  <br><br>
  <label for="currencySymbol"></label>
  <select v-model="currencySymbol">
    <option value="$">Dollars</option>
    <option value="€">Euros</option>
  </select>
  <YummyMeal
      v-for="meal of meals"
      :name="meal.name"
      :price="meal.price"
      @addToCart="addItemToCart"
      :currencySymbol="currencySymbol"
  ></YummyMeal>
</template>

<script>
import YummyMeal from "./components/YummyMeal.vue";
import { ref, reactive, watch, provide } from "vue";
export default {
  components: { YummyMeal },
  setup() {
    const currencySymbol = ref('$')
    provide('currencySymbol', currencySymbol)
    const cart = reactive([])
    const name = ref("The Snazzy Burger")
    const meal = reactive({ name: "Burger", price: 5 })
    const meals = reactive([
      { name: "Burger", price: 5 },
      { name: "Cheeseburger", price: 6 },
      { name: "Impossible Burger", price: 7 },
      { name: "Fries", price: 2 }
    ])
    const placeOrder = () => {
      alert("Your order has been placed!")
    }

    const addItemToCart = (item) => {
      cart.push(item)
    }

    const removeWatcher = watch(() => [...cart], (newItem, oldItem) => alert(newItem.join("\n")))

    return {
      name,
      placeOrder,
      addItemToCart,
      meals,
      removeWatcher,
      currencySymbol
    }
  },
  created() {
    console.log(this.name, "from created")
  }
}
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
