<template>
  <h1>{{ name }}</h1>
  <button @click="placeOrder">Place Order</button>
  <YummyMeal name="Hamburger" price="3" @addToCart="addItemToCart"></YummyMeal>
</template>

<script>
import YummyMeal from "./components/YummyMeal.vue";
export default {
  components: { YummyMeal },
  setup() {
    const name = "The Snazzy Burger";
    const placeOrder = () => {
      alert("Your order has been placed!")
    }

    const addItemToCart = (item) => {
      alert(`One ${item} added to the cart`)
    }

    return {
      name,
      placeOrder,
      addItemToCart
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
