<template>
  <div>
    <nav
      class="navbar is-fixed-top"
      style="background: linear-gradient(221deg, #edc7b7, #eee2dc 73%)"
    >
      <div class="navbar-menu mt-1 mb-1">
        <div class="navbar-start ml-3">
          <div v-if="!user" class="navbar-item">
            <a>
              <router-link to="/register" style="color: #ac3b61"
                >ลงทะเบียน</router-link
              >
              <a class="ml-2 mr-1" style="color: #ac3b61">/</a>
              <router-link to="/login" style="color: #ac3b61">
                เข้าสู่ระบบ</router-link
              >
            </a>
          </div>
          <div v-else class="navbar-item">
            <a>
              <router-link
                :to="`/Profile_user/${user.id}`"
                style="color: #ac3b61"
                >โปรไฟล์</router-link
              >
              <a class="ml-2 mr-1" style="color: #ac3b61">/</a>
              <a @click="Logout" style="color: #ac3b61">
                ออกจากระบบ</a
              >
            </a>
          </div>
        </div>

        <div class="navbar-canter">
          <div class="navbar-item mt-2" style="margin-right: 100px">
            <span class="icon is-size-5 mr-2"
              ><i class="fas fa fa-home" style="color: #ac3b61"></i>
            </span>
            <router-link to="/" style="color: #ac3b61">E5-book</router-link>
          </div>
        </div>

        <div class="navbar-end">
          <p class="navbar-item">
            <router-link to="/Cart_Book" style="color: #ac3b61"
              ><button class="button">
                <span style="color: #ac3b61">ไปหน้ารถเข็น</span>
                <span class="icon is-size-5 ml-2"
                  ><i class="fas fa-shopping-cart" style="color: #ac3b61"> </i
                ></span>
              </button>
            </router-link>
          </p>
        </div>
      </div>
    </nav>
    <br />
    <br />
  </div>
</template>
<script>
import axios from "@/plugins/axios";
export default {
  data() {
    return {
      user: null,
      name: "NavBar",
    };
  },
  mounted() {
    this.onAuthChange();
  },
  methods: {
    onAuthChange() {
      const token = localStorage.getItem("token");
      if (token) {
        this.getUser();
      }
    },
    getUser() {
      axios.get("http://localhost:3000/user/me").then((res) => {
        this.user = res.data;
      });
    },
    Logout() {
      axios
        .delete("http://localhost:3000/user/logout/")
        .then(() => {
          window.localStorage.clear();
          this.user = null
          this.$router.push({ path: "/" });
        })
        .catch((error) => {
          this.error = error.response;
        });
    },
  },
};
</script>
<style >
</style>