<template>
  <div class="hero-body is-fullheight">
    <NavBar />
    <div class="columns is-centered hero-body">
      <div class="column is-half">
        <div class="column has-text-centered">
          <figure class="image">
            <img :src="promotion[0].promotionimage" />
          </figure>
          <br />

          <p class="title is-5">{{ promotion[0].title }}</p>
          <br />
          <p class="subtitle is-6">
            {{ promotion[0].desc }} <br />
            <br />
            โค้ดโปรโมชั่น: {{ promotion[0].code }}
          </p>

          <p class="level-centere">
            <router-link to="/">
              <button
                class="button"
                style="color: #eee2dc; background-color: #ac3b61"
              >
                กลับไปหน้าเลือกซื้อหนังสือ
              </button></router-link
            >
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import NavBar from "@/components/NavBar";
import axios from "axios";
export default {
  name: "DetailPromotion",
  components: {
    NavBar,
  },
  data() {
    return {
      promotion: {
        0: {},
      },
    };
  },
  mounted() {
    this.getpromotionDetail(this.$route.params.id);
  },
  methods: {
    async getpromotionDetail(slideid) {
      await axios
        .get(`http://localhost:3000/DetailsPromotion/${slideid}`)
        .then((response) => {
          this.promotion = response.data;
        })
        .catch((error) => {
          this.error = error.response.data.message;
        });
    },
  },
};
</script>