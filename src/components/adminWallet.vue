<template>
  <div class="hello">
    <div>total SDG: {{ balance }}</div>
    <table>
      <thead>
        <tr>
          <th>email</th>
          <th>username</th>
          <th>balance</th>
        </tr>
      </thead>
      <tbody>
        <div class="inline-block p-8 text-center">
          <div class="font-bold tracking-wide text-gray-800">
            <div class="relative">
              <input
                v-model="search"
                name="search users"
                type="text"
                placeholder="search"
              />
            </div>
          </div>
        </div>
        <tr v-for="user in displayusers" :key="user._id">
          <td>{{ user.email }}</td>
          <td>{{ user.username }}</td>
          <td>{{ user.balance }}</td>
        </tr>
      </tbody>
    </table>
    <nav aria-label="...">
      <paginate
        v-model="page"
        :page-count="pages.length"
        :page-range="3"
        :margin-pages="1"
        :click-handler="clickCallback"
        :prev-text="'Prev'"
        :next-text="'Next'"
        :container-class="'pagination'"
        :page-class="'page-item'"
      >
      </paginate>
    </nav>
    <div>
      <div style="padding: 1%">
        enter email <input v-model="email" type="text" />
      </div>
      <div style="padding: 1%">
        inter debt - <input v-model="debt" type="text" />
      </div>
      <div style="padding: 1%">
        inter crdet + <input v-model="crdet" type="text" />
      </div>
      <div style="padding: 1%">
        <button style="margin: 2%" class="btn btn-danger" @click="fordebt">
          debt
        </button>
        <button class="btn btn-primary" @click="forcrdet">crdet</button>
      </div>
    </div>
  </div>
</template>

<script>
import AuthenticationServices from "@/services/AuthenticationServices";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      balance: "",
      users: [],
      email: "",
      debt: "",
      crdet: "",
      page: 1,
      perPage: 10,
      pages: [],
      search: "",
    };
  },
  async created() {
    const response = await AuthenticationServices.getUsersbalance();
    this.balance = response.data.sum;
    this.users = response.data.orders;
  },
  methods: {
    async fordebt() {
      const useremail = this.email.toLowerCase();
      await AuthenticationServices.debtUsersbalance({
        balance: this.debt,
        email: useremail,
      });
    },
    async forcrdet() {
      const useremail = this.email.toLowerCase();
      await AuthenticationServices.crdetUsersbalance({
        balance: this.crdet,
        email: useremail,
      });
    },
    paginate(users) {
      let page = this.page;
      let perPage = this.perPage;
      let from = page * perPage - perPage;
      let to = page * perPage;
      return users.slice(from, to);
    },
    setusers() {
      let numberOfPages = Math.ceil(this.users.length / this.perPage);
      for (let i = 1; i <= numberOfPages; i++) {
        this.pages.push(i);
      }
    },
  },
  computed: {
    displayusers() {
      return this.paginate(this.users).filter((p) => {
        return p.email.toLowerCase().indexOf(this.search.toLowerCase()) != -1;
      });
    },
  },
  watch: {
    users() {
      this.setusers();
    },
  },
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
