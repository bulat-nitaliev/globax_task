<template>
  <div class="container">
    <nav></nav>
    <div class="base">
      <div class="input-group mb-3 mt-5">
        <input
          type="text"
          class="form-control"
          aria-label="Username"
          aria-describedby="basic-addon1"
          v-model="searchQuery"
          @input="searchName"
        />
        <img src="@/assets/lupa.svg" alt="" />
      </div>
      <div class="user_cards">
        <div
          class="card"
          style="width: 18rem; height: 18rem"
          v-for="user in data_users"
          :key="user"
          @click="getUserOne(user.name)"
        >
          <div class="card-body">
            <h5 class="card-title">{{ user.name }}</h5>
            <div class="contact">
              <img src="@/assets/phone.svg" alt="" />
              <p class="card-text">
                {{ user.phone }}
              </p>
            </div>
            <div class="contact">
              <img src="@/assets/post.svg" alt="" />
              <p class="card-text">
                {{ user.email }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <my-dialog v-model:show="isVisible">
      <user :users="users" :isVisible="showDialog"></user>
    </my-dialog>
  </div>
</template>

<script>
import User from "@/components/User.vue";
import $api from "@/http";
export default {
  components: {
    User,
  },
  data() {
    return {
      data_users: [],
      searchQuery: "",
      isVisible: false,
      users: [],
    };
  },
  methods: {
    async getUsers() {
      const response = await $api.get("/");
      console.log(response.data);
      this.data_users = response.data;
    },
    searchName() {
      this.data_users = this.data_users.filter((user) =>
        user.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
    getUserOne(val) {
      this.isVisible = true;
      this.users = this.data_users.filter((user) =>
        user.name.toLowerCase().includes(val.toLowerCase())
      );
    },
    showDialog() {
      this.isVisible = false;
    },
  },
  created() {
    this.getUsers();
  },
};
</script>

<style>
.user_cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.card {
  margin-top: 15px;
  border-radius: 5%;
}
.card-title {
  font-family: "Proxima Nova";
  font-weight: bold;
  padding-bottom: 30px;
}
.contact {
  display: flex;
  justify-content: start;
  margin-top: 10px;
  gap: 10px;
}

.form-control {
  border: none;
  outline: none;
  outline-offset: 0;
  margin: 10px;
}
.input-group {
  border: 1px solid gray;
  border-radius: 20px;
  height: 48px;
  display: flex;
  align-content: center;
  padding: 10px;
}
.dialog {
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  display: flex;
}
</style>
