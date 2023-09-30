<template>
  <div class="wave">
    <div class="card">
      <div class="card-body">
        <img :src="imageUrl" alt="Jaket" />
        <div class="content">
          <h1 ref="title">jaket adalah salah satu pakian yang sangat khas di indoneisa pakaian ini sangat amat di minati oleh orang orang asia</h1>
          <div class="category">
            <p ref="category">women</p>
            <div class="ratting">
              <p class="ratting-text">2.9/15</p>
              <span class="dot" id="dot-collor"></span>
              <span class="dot" id="dot-collor"></span>
              <span class="dot"></span>
              <span class="dot"></span>
              <span class="dot"></span>
            </div>
          </div>
          <hr />
          <div class="description">
            <p ref="description">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
              consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
            </p>
          </div>
          <hr />
          <div class="price">
            <h2 ref="price">$29.95</h2>
          </div>
          <div class="button">
            <button class="buy">Buy now</button>
            <button class="next" @click="getNextProduct">Next product</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductDisplay",
  data() {
    return {
      index: 1,
      imageUrl: "",
      loading: true,
      category: "",
    };
  },
  created() {
    fetch(`https://fakestoreapi.com/products/${this.index}`)
      .then((res) => res.json())
      .then((json) => {
        this.loading = false;
        console.log(json);
        const title = json.title;
        const category = json.category;
        const description = json.description;
        const price = json.price;
        if (category == "men's clothing" || category == "women's clothing") {
          this.$refs.category.innerText = category;
          this.$refs.title.innerText = title;
          this.$refs.description.innerText = description;
          this.$refs.price.innerText = "$" + price;
          this.imageUrl = json.image;
        }
      });
  },
  methods: {
    getNextProduct() {
      if (this.index >= 20) {
        this.index = 1; //Reset index jika mecapai 20
      } else {
        this.index++; //index tambah
      }

      // this.loading = true;
      fetch(`https://fakestoreapi.com/products/${this.index}`)
        .then((res) => res.json())
        .then((json) => {
          console.log(json);
          const title = json.title;
          const category = json.category;
          const description = json.description;
          const price = json.price;
          if (category == "men's clothing" || category == "women's clothing") {
            this.$refs.category.innerText = category;
            this.$refs.title.innerText = title;
            this.$refs.description.innerText = description;
            this.$refs.price.innerText = "$" + price;
            this.imageUrl = json.image;
          } else {
            this.getNextProduct();
          }
        })
        .catch((err) => console.error("Error: ", err));
    },
  },
};
</script>

<style src="/src/assets/style/ProductDisplay.css"></style>
