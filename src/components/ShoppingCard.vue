<template>
  <div>
    <div class="bottom">
      <div class="white_bottom">
        <div class="left_side">
          <input class="mouseP" type="text" />
          <div class="top_sq"></div>
          <div class="bottom_sq"></div>
          <div class="shoe">
            <div class="shoe_img">
              <img
                class="imgR"
                :src="product.images[product.colors[selectedColorIndex]]"
              />
            </div>
          </div>
          <div class="switch">
            <div class="switch1 th_shoe"></div>
            <div class="switch2"></div>
          </div>
          <div class="icon">
            <div @click="isVisible = true" class="cart" id="cartIcon">
              <svg viewbox="0 2 50 50">
                <path d="M22.822,28.96"></path>
                <polyline
                  points="15.289,18.241 17.591,18.528 21.689,30 30.228,30 32.208,22.262 18.891,22.325 "
                ></polyline>
                <circle class="w" cx="28.472" cy="32.31" r="0.996"></circle>
                <circle class="w" cx="23.257" cy="32.31" r="0.996"></circle>
                <circle cx="24.804" cy="25.496" r="19.121"></circle>
              </svg>
              <div class="RTnumber">{{ basket.length }}</div>
            </div>
          </div>
        </div>
        <div class="right_side">
          <div class="product">
            <div class="sname">
              &nbsp;{{ product.category }}
              <div class="name">
                <b>{{ product.title }}</b>
              </div>
            </div>
            <div class="price">{{ priceWithShoesNumber }}$</div>
          </div>
          <div class="deco"></div>
          <div class="detail">
            <div class="qua">
              <div class="text">
                <div class="word">Quantity:&nbsp;</div>
                <div class="count">{{ product.quantity }}</div>
              </div>
              <div class="counter">
                <div class="sub" @click="quantityReduce()">-</div>
                <div class="num">{{ product.quantity }}</div>
                <div class="add" @click="quantityIncrement()">+</div>
              </div>
            </div>
            <div class="color">
              <div class="text">
                <div class="word">Color:&nbsp;</div>
                <div class="this_color"></div>
              </div>
              <div class="color_group">
                <div
                  class="c1"
                  v-for="(color, index) in product.colors"
                  :key="index"
                  @click="selectedColorIndex = index"
                  :style="{ backgroundColor: color }"
                ></div>
              </div>
            </div>
            <div class="size">
              <div class="text">
                <div class="this_size">Size:&nbsp;</div>
                <div class="size_num"></div>
              </div>
              <ul>
                <li
                  v-for="(size, index) in product.sizes"
                  :key="index"
                  :class="{ th_size: index == selectedShoesNumberIndex }"
                  @click="selectedShoesNumberIndex = index"
                >
                  {{ size }}
                </li>
              </ul>
            </div>
          </div>
          <button
            id="addTOCart"
            :style="{ background: product.colors[selectedColorIndex] }"
          >
            <svg viewbox="0 0 50 50">
              <path d="M22.822,28.96"></path>
              <polyline
                points="15.289,18.241 17.591,18.528 21.689,30 30.228,30 32.208,22.262 18.891,22.325 "
              ></polyline>
              <circle class="w" cx="28.472" cy="32.31" r="0.996"></circle>
              <circle class="w" cx="23.257" cy="32.31" r="0.996"></circle>
            </svg>
            <h1 @click="addToBasket(product)">
              Add to Cart
            </h1>
          </button>
        </div>
      </div>
      <div v-if="isVisible" class="cart_bottom">
        <div class="cart_list">
          <div @click="isVisible = false" class="close_btn">✖</div>
          <div class="title">
            <div class="cart_icon">
              <svg viewbox="0 0 50 50">
                <path d="M22.822,28.96"></path>
                <polyline
                  points="15.289,18.241 17.591,18.528 21.689,30 30.228,30 32.208,22.262 18.891,22.325 "
                ></polyline>
                <circle class="w" cx="28.472" cy="32.31" r="0.996"></circle>
                <circle class="w" cx="23.257" cy="32.31" r="0.996"></circle>
              </svg>
            </div>
            <h2>Your Cart</h2>
          </div>
          <div class="list">
            <div class="cart_cat">
              <div class="desT">Description</div>
              <div class="colorT">Color</div>
              <div class="sizeT">Size</div>
              <div class="QTYT">QTY</div>
              <div class="priceT">Price</div>
            </div>
            <ul>
              <li v-for="(product, index) in basket" :key="index">
                <div class="i_des">
                  <div class="pimg"><img :src="product.selectedImage" /></div>
                  <div class="i_name">{{ product.name }}</div>
                  <div class="i_date">.</div>
                </div>
                <div class="i_color">
                  {{ product.colors[selectedColorIndex] }}
                </div>
                <div class="i_size">
                  {{ product.sizes[selectedShoesNumberIndex] }}
                </div>
                <div class="i_QTY">
                  {{ product.quantity }}
                </div>
                <div class="i_price">
                  {{ product.newPrice * product.quantity }}
                </div>
              </li>
            </ul>
          </div>
          <div class="total">
            <div class="totalT">Total:</div>
            <div class="totalP">{{ totalPrice }}</div>
          </div>
          <div class="checkout">
            <button @click="isVisible = false" class="cancel">Cancel</button>
            <button>Checkout</button>
          </div>
        </div>
      </div>
    </div>
    <div class="roomRec">
      <div class="recbottom"></div>
      <img src="" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    product: null,
    basket: [],
  },
  data() {
    return {
      selectedShoesNumberIndex: 0,
      selectedColorIndex: 0,
      selectedQuantityIndex: 0,
      isVisible: false,
    };
  },
  methods: {
    quantityIncrement() {
      if (this.product.quantity >= 10) return;
      this.product.quantity++;
    },
    quantityReduce() {
      if (this.product.quantity <= 1) return;
      this.product.quantity--;
    },
    addToBasket(val) {
      this.$emit("addProduct", {
        ...val,
        selectedImage: this.product.images[
          this.product.colors[this.selectedColorIndex]
        ],
        newPrice: this.priceWithShoesNumber,
      });
    },
  },
  computed: {
    priceWithShoesNumber() {
      return (
        100 +
        (this.product.sizes[this.selectedShoesNumberIndex] *
          this.product.sizes[this.selectedShoesNumberIndex]) /
          10
      );
    },
    totalPrice() {
      let price = 0;

      this.basket.forEach((p) => (price += p.newPrice * p.quantity));
      return price;
    },
  },
};
</script>

<style>
@import "../assets/styles/CardStyle.css";
</style>
