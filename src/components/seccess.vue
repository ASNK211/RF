<template>
  <div id="app">
    <div class="self-building-square-spinner">
      <div class="square"></div>
      <div class="square"></div>
      <div class="square"></div>
      <div class="square clear"></div>
      <div class="square"></div>
      <div class="square"></div>
      <div class="square clear"></div>
      <div class="square"></div>
      <div class="square"></div>
    </div>
  </div>
</template>

<script>
import AuthenticationServices from "@/services/AuthenticationServices";
// import axios from "axios";
// import EventBus from '@/event-bus.js'
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  async created() {
    // console.log("response.data");
    // const response = await axios.get("http://localhost:8800/api/seccess", {
    //   withCredentials: true,
    // });
    // console.log(response);

    // axios.get("http://localhost:8800//seccess")
    const response = await AuthenticationServices.getseccess();
    // .then((response) => {
    // console.log("response");
    // // console.log(response.data)
    // console.log(response.data.sendUser)
    // })
    // .catch(function (error) {
    // console.log(error);
    // });
    console.log("response.data");
    console.log(response);
    console.log(response.data);
    localStorage.setItem("isAdmin", response.data.sendUser.isAdmin);
    localStorage.setItem("email", response.data.sendUser.email);
    localStorage.setItem("token", response.data.accessToken);
    localStorage.setItem("userId", JSON.stringify(response.data.sendUser._id));
    this.$store.dispatch("setToken", response.data.accessToken);
    this.$store.dispatch("setUser", response.data.sendUser);
    this.$store.dispatch("setAdmin", response.data.sendUser.isAdmin);
    const dddd = response.data;
    console.log("ddd", dddd);
    if (dddd) {
      // this.$root.$emit('myEvent', "response.data.accessToken");
      setTimeout(() => {
        // location.reload();
        // window.close();
        window.location.href = "https://zoolgame.com/";
      }, 1000);
    }

    // EventBus.$emit('event-name',response.data.accessToken)
  },
  // created() {
  //   setTimeout(() => {
  //     window.close();
  //   }, 10);
  // },
};
</script>

<style scoped lang="scss">
#app {
  background-color: #2c263c;
  position: absolute;
  z-index: 1000;
  /* background-color: white; */
  height: 120%;
  width: 100%;
  right: 0px;
  top: 0px;
  /* bottom: 0px; */
  /* padding: 100%; */
  text-align: center;
  line-height: 1000vh;
}

@media (max-width: 760px) {
  #app {
    background-color: #2c263c;
    position: absolute;
    z-index: 1000;
    /* background-color: white; */
    height: 250%;
    width: 100%;
    right: 0px;
    top: 0px;
    /* bottom: 0px; */
    /* padding: 100%; */
    text-align: center;
    line-height: 100vh;
  }
  .self-building-square-spinner,
  .self-building-square-spinner * {
    box-sizing: border-box;
    position: relative;
    margin: auto;
    margin-top: 50%;
  }

  .self-building-square-spinner {
    height: 40px;
    width: 40px;
    top: calc(-10px * 2 / 3);
  }

  .self-building-square-spinner .square {
    height: 10px;
    width: 10px;
    top: calc(-10px * 2 / 3);
    margin-right: calc(10px / 3);
    margin-top: calc(10px / 3);
    background: #ff1d5e;
    float: left;
    position: relative;
    opacity: 0;
    animation: self-building-square-spinner 6s infinite;
  }

  .self-building-square-spinner .square:nth-child(1) {
    animation-delay: calc(300ms * 6);
  }

  .self-building-square-spinner .square:nth-child(2) {
    animation-delay: calc(300ms * 7);
  }

  .self-building-square-spinner .square:nth-child(3) {
    animation-delay: calc(300ms * 8);
  }

  .self-building-square-spinner .square:nth-child(4) {
    animation-delay: calc(300ms * 3);
  }

  .self-building-square-spinner .square:nth-child(5) {
    animation-delay: calc(300ms * 4);
  }

  .self-building-square-spinner .square:nth-child(6) {
    animation-delay: calc(300ms * 5);
  }

  .self-building-square-spinner .square:nth-child(7) {
    animation-delay: calc(300ms * 0);
  }

  .self-building-square-spinner .square:nth-child(8) {
    animation-delay: calc(300ms * 1);
  }

  .self-building-square-spinner .square:nth-child(9) {
    animation-delay: calc(300ms * 2);
  }

  .self-building-square-spinner .clear {
    clear: both;
  }

  @keyframes self-building-square-spinner {
    0% {
      opacity: 0;
    }
    5% {
      opacity: 1;
      top: 0;
    }
    50.9% {
      opacity: 1;
      top: 0;
    }
    55.9% {
      opacity: 0;
      top: inherit;
    }
  }
}
.self-building-square-spinner,
.self-building-square-spinner * {
  box-sizing: border-box;
  position: relative;
  margin: auto;
  margin-top: 20%;
}

.self-building-square-spinner {
  height: 40px;
  width: 40px;
  top: calc(-10px * 2 / 3);
}

.self-building-square-spinner .square {
  height: 10px;
  width: 10px;
  top: calc(-10px * 2 / 3);
  margin-right: calc(10px / 3);
  margin-top: calc(10px / 3);
  background: #ff1d5e;
  float: left;
  position: relative;
  opacity: 0;
  animation: self-building-square-spinner 6s infinite;
}

.self-building-square-spinner .square:nth-child(1) {
  animation-delay: calc(300ms * 6);
}

.self-building-square-spinner .square:nth-child(2) {
  animation-delay: calc(300ms * 7);
}

.self-building-square-spinner .square:nth-child(3) {
  animation-delay: calc(300ms * 8);
}

.self-building-square-spinner .square:nth-child(4) {
  animation-delay: calc(300ms * 3);
}

.self-building-square-spinner .square:nth-child(5) {
  animation-delay: calc(300ms * 4);
}

.self-building-square-spinner .square:nth-child(6) {
  animation-delay: calc(300ms * 5);
}

.self-building-square-spinner .square:nth-child(7) {
  animation-delay: calc(300ms * 0);
}

.self-building-square-spinner .square:nth-child(8) {
  animation-delay: calc(300ms * 1);
}

.self-building-square-spinner .square:nth-child(9) {
  animation-delay: calc(300ms * 2);
}

.self-building-square-spinner .clear {
  clear: both;
}

@keyframes self-building-square-spinner {
  0% {
    opacity: 0;
  }
  5% {
    opacity: 1;
    top: 0;
  }
  50.9% {
    opacity: 1;
    top: 0;
  }
  55.9% {
    opacity: 0;
    top: inherit;
  }
}
</style>
