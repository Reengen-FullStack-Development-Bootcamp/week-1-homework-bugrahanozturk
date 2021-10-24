<template>
  <div>
    <ShoppingCard
      v-for="(item, i) in CardInfoList"
      :key="i"
      :product="item"
      @addProduct="addProduct"
      :basket="basket"
    />
  </div>
</template>

<script>
import ShoppingCard from "./components/ShoppingCard.vue";

export default {
  components: {
    ShoppingCard,
  },
  data() {
    return {
      CardInfoList: [
        {
          category: "Sport Shoes",
          title: "Nike Epic React ",
          images: {
            burlywood: require("./assets/1-shoes.png"),
            blue: require("./assets/blue-shoes.png"),
            red: require("./assets/red-shoes.png"),
            black: require("./assets/black-shoes.png"),
          },
          colors: ["burlywood", "blue", "red", "black"],
          price: 100,
          sizes: [40, 41, 43, 44, 45],
          quantity: 1,
        },
      ],
      basket: [],
    };
  },
  methods: {
    addProduct(e) {
      this.basket.unshift(e);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
