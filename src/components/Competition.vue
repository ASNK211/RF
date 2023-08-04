<template>
  <div class="maindiv">
    <div class="equlte">
      <div v-if="istrue.inCompetition === false">
        <button @click="competiton" class="Competitionbuttun">
          اشترك مجانا
        </button>
        <h1 class="postone">
          تنافس مع المشترين الاخرين وخذ المرتبه الاوليعن طريق شراء اكبر كميه من
          منتجاتنا
        </h1>
      </div>
      <div
        v-for="(user, index) in users"
        :key="index"
        :class="{
          'yellow-background': index === 0,
          'black-background': index === 1,
          'bronze-background': index === 2,
        }"
        class="usersin"
      >
        <h1 class="username">{{ user.username }}:</h1>
        <h1>{{ user.monthbalance }}</h1>
      </div>
    </div>
  </div>
</template>

<script>
import AuthenticationServices from "@/services/AuthenticationServices";
export default {
  name: "AddToCart",
  data() {
    return {
      users: [],
      istrue: [],
    };
  },
  async created() {
    const response = await AuthenticationServices.getcompetiton();
    this.users = response.data;
    const userId = localStorage.getItem("userId");
    const respons = await AuthenticationServices.getUsercompetiton(userId);
    this.istrue = respons.data;
  },
  methods: {
    async competiton() {
      const userId = localStorage.getItem("userId");
      await AuthenticationServices.competiton({
        userId: userId,
      }).then(() => {
        window.location.reload();
      });
    },
  },
};
</script>
<style scoped lang="scss">
.Competitionbuttun {
  background-color: #48db58;
  border-radius: 5px;
  padding: 4px;
}
.maindiv {
  margin-top: 5;
  padding-bottom: 20px;
}
.equlte {
  position: relative;
  top: 50px;
  overflow: auto;
  height: 1000px;
  padding-bottom: 200px;
}
.usersin {
  border: 1px solid #b9b9b9;
  width: 66%;
  position: relative;
  left: 18%;
  top: 10px;
  border-radius: 10px;
  margin: 5px;
  font-size: 19px;
  font-weight: 600;
  background-color: burlywood;
  height: 31px;
}
h1 {
  display: inline-block;
}
.firstone {
  border: 1px solid #f0e20e;
  height: 45px;
  position: absolute;
  top: 36px;
  width: 98%;
  z-index: -1;
  background-color: #fffc40;
  left: 2px;
}
.username {
  width: 153px;
  position: relative;
  right: 54px;
}
.yellow-background {
  background-color: #ffd700;
  font-weight: bolder;
  font-size: 30px;
  height: 49px;
  position: relative;
  top: 10px;
  width: 77%;
  left: 12%;
}
.black-background {
  background-color: #c0c0c0;
  font-weight: bold;
  font-size: 23px;
  border: 1px #c0c0c0 solid;
  height: 40px;
  width: 73%;
  position: relative;
  left: 14%;
  box-shadow: 0px 4px #f7f2f2;
}
.bronze-background {
  background-color: #cd7f32;
  font-weight: bold;
  font-size: 22px;
  border: 1px #c0c0c0 solid;
  height: 37px;
  width: 71%;
  position: relative;
  left: 15%;
  box-shadow: 0px 4px #f7f2f2;
}
.postone {
  font-weight: bold;
  color: black;
}
</style>
