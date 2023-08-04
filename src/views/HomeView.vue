<template>
  <div class="bg-gray-100">
    <div class="divtaitle">
      <h1 class="titale">
        <span class="toptitle">متجرك الإلكتروني</span>
        <span class="bottomtitle">حيث تجد جميع العابك المفضله</span>
      </h1>
    </div>
    <div
      style="
        display: flex;
        justify-content: center;
        height: 40%;
        padding: 2%;
        padding-bottom: 16%;
        position: relative;
        top: 28px;
      "
    >
      <img
        id="rightimage"
        class="imagespr"
        src="./img/Garena-Free-Fire.jpg"
        alt="zoolgame"
      />
      <div class="rendo">
        <img
          class="imagespr"
          src="./img/pubg1.jpg"
          alt="zoolgame"
          id="midaleimage"
        />
      </div>
      <img
        id="leftimage"
        class="imagespr"
        src="./img/xbox.jpg"
        alt="zoolgame"
      />
    </div>
    <h2 class="index-title">المنتجات</h2>
    <!-- Remove py-8 -->
    <LoadingScreen v-if="isLoading"></LoadingScreen>
    <div class="mx-auto container py-8">
      <div class="card1">
        <div
          v-for="product in products"
          :key="product._id"
          class="card"
          style="border: 1px solid #e2ebf2"
        >
          <div>
            <img :src="`${urlimage}${product.image}`" class="themainimge" />
          </div>
          <div class="bg-white p-2">
            <h2 class="text-lg font-semibold">
              {{ product.name }}
            </h2>
            <div>
              <p class="text-xs text-gray-600 mt-2">
                <router-link
                  :to="`/${product.productname}`"
                  class="btn btn-primary"
                  >اطلب الان</router-link
                >
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import LoadingScreen from "../components/lodingPage.vue";
import AuthenticationServices from "@/services/AuthenticationServices";
import axios from "axios";
export default {
  name: "HomeView",
  data() {
    return {
      products: [],
      isLoading: true,
      urlimage: "",
    };
  },
  components: {
    LoadingScreen,
  },
  async created() {
    this.urlimage = process.env.VUE_APP_IMMAGE_CLIENT;
    const respons = await AuthenticationServices.getintproduct();
    this.products = respons.data;
    if (this.products) {
      this.isLoading = false;
    }
    //     const isaAdmin = localStorage.getItem("isAdmin");
    // console.log(Boolean(isaAdmin === "true"))
    const response = await axios.get(`${process.env.VUE_APP_SUCCESS}`, {
      withCredentials: true,
    });
    // console.log(response.data);
    localStorage.setItem("isAdmin", response.data.sendUser.isAdmin);
    localStorage.setItem("email", response.data.sendUser.email);
    localStorage.setItem("token", response.data.accessToken);
    localStorage.setItem("userId", JSON.stringify(response.data.sendUser._id));
    this.$store.dispatch("setToken", response.data.accessToken);
    this.$store.dispatch("setUser", response.data.sendUser);
    this.$store.dispatch("setAdmin", response.data.sendUser.isAdmin);
    // if (response.data.sendUser._id) {
    //   window.location.reload();
    // }
    // const dddd = response.data;
  },
  methods: {
    // lodin(){
    //   if(this.products) {
    //     this.isLoading = false;
    //   }
    // }
  },
  // mounted() {
  //   setTimeout(() => {
  //     this.isLoading = false;
  //   }, 9500);
  // }
  mounted() {
    document.title = "Home";
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+Arabic:wght@500&display=swap");
div {
  font-family: "Noto Sans Arabic", sans-serif;
}

@media (max-width: 767px) {
  .card {
    display: inline-block;
    /* flex: 1 1 auto; */
    width: 50%;
    margin-top: 10px;
    border-radius: 15px;
  }
  .themainimge {
    width: 100%;
    height: 155px;
    border-radius: 11px;
  }
}
@media (min-width: 768px) {
  .card {
    display: inline-block;
    /* flex: 1 1 auto; */
    width: 25%;
    margin-top: 10px;
  }
  .themainimge {
    width: 100%;
    height: 120px;
  }
}
@media (max-width: 767px) {
  .rendo {
    display: flex;
    z-index: 2;
    width: 35%;
    position: absolute;
  }
  #midaleimage {
    position: relative;
    top: 58px;
    width: 100%;
  }
  .imagespr {
    border-radius: 8px;
    width: 37%;
    position: relative;
    top: 38px;
    height: 80px;
  }
}
@media (min-width: 768px) {
  .rendo {
    display: flex;
    z-index: 2;
    width: 35%;
    position: absolute;
  }
  #midaleimage {
    position: relative;
    top: 118px;
    width: 100%;
  }
}
.toptitle {
  display: block;
  background-image: linear-gradient(to right, #eb1d5a, #f91212);
  color: #e2521b;
  /* font-size: 53px; */
  line-height: 1;
  margin-bottom: 21px;
  max-width: 100%;
  text-transform: uppercase;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
.bottomtitle {
  font-size: 62%;
}
.divtaitle {
  background-image: none;
  display: flex;
  grid-row: 1;
  margin: auto;
  text-align: center;
  position: relative;
  top: 59px;
}
.titale {
  color: #5e5e5e;
  font-size: 36px;
  font-weight: 400;
  line-height: 1.2;
  margin: auto;
}
.index-title {
  color: #c1c1c1;
  font-size: 24px;
  margin: 32px 0 16px;
  text-transform: uppercase;
  font-weight: 400;
  position: relative;
  top: 19px;
}
#rightimage {
  position: relative;
  right: 40px;
}
#leftimage {
  position: relative;
  left: 40px;
}
.imagespr {
  border-radius: 8px;
  width: 37%;
  position: relative;
  top: 38px;
}
.card1 {
  display: flex;
  justify-content: space-around;
  /* flex: auto; */
  /* gap: 10px; */
  /* gap: 10px 20px; row-gap column gap */
  /* row-gap: 10px;
  column-gap: 20px; */
  /* flex-grow: 2; */
  flex-wrap: wrap;
  /* flex-flow: column wrap; */
}
/* .container {
  padding-bottom: 8%;
}
.product-list {
  background-color: rgb(190, 190, 190);
  padding: 3em;
}
.product-list .card {
  background-color: white;
  border-radius: 10px;
  padding: 1em;
  box-shadow: 0px 10px 5px #b2bec3;
  text-align: center;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}
.card .title {
  font-size: 18px;
  font-weight: bold;
}
.card img {
  max-width: 80%;
  border-radius: 10px;
}
.card .text {
  text-align: left;
  margin-left: 2em;
  margin-bottom: 0.5em;
  font-size: 12px;
}
.product-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-column-gap: 20px;
  grid-row-gap: 40px;
}
@media (max-width: 760px) {
  .product-container {
    display: grid;
    grid-template-columns: 1fr;
    grid-column-gap: 20px;
    grid-row-gap: 40px;
  }
}
.zoolimge {
  border-radius: 30%;
  width: 10%;
  height: 10%;
  padding-bottom: 2%;
}
h4 {
  color: red;
  font: 600;
} */
</style>
