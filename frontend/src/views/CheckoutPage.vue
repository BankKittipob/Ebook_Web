<template>
  <div>
    <NavBar />
    <div class="hero-body hero is-fullheight">
      <div class="container has-text-centered">
        <div class="column">
          <p class="is-size-3" style="color: #ac3b61">เลือกวิธีการ ชำระเงิน</p>
          <br />
          <div class="divider is-info" style="color: #123c69">
            Choose a payment
          </div>
        </div>
        <div class="box" style="width: 800px">
          <article class="media">
            <div class="media-left">
              <img
                src="https://www.kasikornbank.com/SiteCollectionDocuments/about/img/logo/logo.png"
                alt="Image"
                class="image is-64x64"
              />
            </div>
            <div class="media-content">
              <div class="content">
                <p>
                  ธนาคาร กสิกรไทย
                  <br />
                  ชื่อบัญชี : หนังสือออนไลน์ อีไฟท์บุค
                  <br />
                  เลขที่บัญชี : 0498765793
                </p>
              </div>
            </div>
          </article>
        </div>
        <div class="box">
          <article class="media">
            <div class="media-left">
              <img
                src="https://www.finnomena.com/wp-content/uploads/2016/10/promt-pay-logo.jpg"
                class="image is-64x64"
              />
            </div>
            <div class="media-content">
              <div class="content">
                <p>
                  พร้อมเพย์
                  <br />
                  ชื่อบัญชี : หนังสือออนไลน์ อีไฟท์บุค
                  <br />
                  รหัสพร้อมเพย์ : 0999728955
                </p>
              </div>
            </div>
          </article>
        </div>
        <div class="box">
          <article class="media">
            <div class="media-left">
              <img
                src=" https://seeklogo.com/images/T/truemoney-wallet-logo-9CCDDD6CB0-seeklogo.com.png"
                class="image is-64x64"
              />
            </div>
            <div class="media-content">
              <div class="content">
                <p>
                  ทรูมันนี่วอลเล็ท
                  <br />
                  ชื่อบัญชี : หนังสือออนไลน์ อีไฟท์บุค
                  <br />
                  เบอร์ทรูมันนี่วอลเล็ท : 0999728955
                </p>
              </div>
            </div>
          </article>
        </div>
      </div>

      <div class="container has-text-centered mt-6">
        <div class="column">
          <p class="is-size-3" style="color: #ac3b61">โค้ดโปรโมชั่น</p>
          <br />
          <div class="divider is-info" style="color: #123c69">
            Choose a payment
          </div>
        </div>
        <div class="box" style="width: 800px">
          <article class="media">
            <div class="media-content">
              <label class="label" style="color: #123c69"
                >กรอกโค้ดโปรโมชั่น จำกัดหนึ่งโค้ดต่อ 1 ตะกร้า</label
              >
              <input
                class="input is-medium is-rounded"
                type="text"
                v-model="Promotion"
                v-if="checkcode == 0"
              />
              <input
                class="input is-medium is-rounded"
                type="text"
                v-model="Promotion"
                disabled
                v-if="checkcode == 1"
              />

              <div class="level mt-4">
                <button
                  v-if="checkcode == 0"
                  class="button"
                  style="color: #eee2dc; background-color: #ac3b61"
                  @click="submitPromotion(Cart_item[0].cart_id)"
                >
                  ใช้โค้ดโปรโมชั่น
                </button>

                <button
                  v-if="checkcode == 1"
                  class="button"
                  style="color: #eee2dc; background-color: #ac3b61"
                  @click="canceltPromotion(Cart_item[0].cart_id)"
                >
                  ยกเลิกโค้ดโปรโมชั่น
                </button>
              </div>
            </div>
          </article>
        </div>
        <div class="divider is-info is-size-6" style="color: #123c69">
          <router-link to="/Cart_Book" style="color: #123c69"
            >กลับไปหน้าตะกร้า หนังสือ</router-link
          >
        </div>
      </div>

      <div class="container hero-body">
        <div class="columns is-multiline box">
          <div class="column">
            <h1 class="title has-text-centered section-title is-size-5">
              สรุปรายการสั่งซื้อ
            </h1>
            <div class="box" v-for="card in Cart_item" v-bind:key="card.id">
              <article class="media" v-if="Cart_item.length > 0">
                <div class="media-left">
                  <img
                    :src="'http://localhost:3000/' + card.image"
                    alt="Image"
                    style="object-fit: cover"
                    class="image is-64x64"
                  />
                </div>
                <div class="media-content">
                  <div class="content">
                    <p>
                      <strong>{{ card.title }}</strong>
                      <br />
                      <small>{{ card.price }} บาท</small>
                    </p>
                  </div>
                </div>
              </article>
            </div>

            <h1 class="title has-text-centered section-title is-size-5">
              ยอดชำระเงิน(รวมใช้โค้ดโปรโมชั่น) :
              {{ total }} บาท
            </h1>
          </div>
          <div class="column is-10 has-text-centered is-offset-1">
            <h2 class="subtitle">
              จำนวนหนังสือซื้อที่ซื้อ : {{ Cart_item.length }} เล่ม
            </h2>
            <button class="button" @click="Payment = true">
              ยืนยันรายการชำระเงิน&emsp;<i
                class="fa fa-check"
                aria-hidden="true"
              ></i>
            </button>
          </div>
        </div>
      </div>

      <div class="modal" :class="{ 'is-active': Payment }">
        <div class="modal-background"></div>
        <div class="modal-card">
          <button
            class="modal-close is-large"
            aria-label="close"
            @click="Payment = false"
          ></button>

          <section class="modal-card-body">
            <div class="field">
              <span
                class="label is-size-5"
                style="color: #123c69; text-align: center"
              >
              </span>
              <h1 class="title has-text-centered section-title is-size-5">
                ยอดชำระเงิน(รวมใช้โค้ดโปรโมชั่น) : {{ this.total }} บาท
              </h1>
              เมื่อโอนเสร็จ กรุณาส่งสรีปการชำระเงิน
              <div class="column is-5">
                <div class="file">
                  <label class="file-label">
                    <input
                      type="file"
                      accept="image/png, image/jpeg, image/webp"
                      @change="selectImages"
                      class="file-input"
                    />
                    <span class="file-cta">
                      <span class="file-icon">
                        <i class="fas fa-upload"></i>
                      </span>
                      <span class="file-label"> Choose an image</span>
                    </span>
                  </label>
                </div>
              </div>
            </div>
          </section>
          <footer class="modal-card-foot">
            <button
              class="button is-success"
              @click="submitpay(Cart_item[0].cart_id)"
            >
              ส่งข้อมูล
            </button>
            <button class="button" @click="Payment = false">ยกเลิก</button>
          </footer>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import NavBar from "@/components/NavBar";
import axios from "@/plugins/axios";

export default {
  name: "CheckoutPage",
  components: {
    NavBar,
  },
  data() {
    return {
      Payment: false,
      Promotion: "",
      promotioncheck: {
        0: {},
      },
      num: 0,
      Cart_item: {
        0: {},
      },
      checkcode: 0,
      total: 0,
      codenum: 0,
      numcheck: true,
      keepnum: 0,
      images: [],
    };
  },
  async mounted() {
    await this.getItems(this.$route.params.id);
  },
  methods: {
    async getItems() {
      await axios
        .get("http://localhost:3000/getCartItem", {
          params: {
            search: this.search,
          },
        })
        .then((response) => {
          this.Cart_item = response.data;
          this.total = response.data[0].total_price;
          this.keepnum = response.data[0].total_price;
          console.log(this.Cart_item);
        })
        .catch((err) => {
          console.log(err);
        });
      await axios
        .get(`http://localhost:3000/promotion_image`)
        .then((response) => {
          this.promotioncheck = response.data;
          console.log(this.promotioncheck);
        })
        .catch((error) => {
          this.error = error.response.data.message;
        });
    },
    async submitPromotion(cartid) {
      if (this.promotioncheck.find((x) => x.code == this.Promotion)) {
        await axios
          .put(`http://localhost:3000/submitPromotion`, {
            cart_id: cartid,
            codepromotion: this.Promotion,
          })
          .then((response) => {
            this.checkcode = 1;
            this.Promotion = "";
            this.codenum = response.data;
          })
          .catch((err) => {
            console.log(err);
          });
        alert("ใช้โค้ดสำเร็จแล้ว");
        if (
          this.checkcode == 1 &&
          this.promotioncheck[this.codenum - 1].promotioncol == ">" &&
          this.total >= this.promotioncheck[this.codenum - 1].amont
        ) {
          console.log("1");
          this.total =
            (this.total *
              this.promotioncheck[this.codenum - 1].percentpromotion) /
            100;
        } else if (
          this.checkcode == 1 &&
          this.promotioncheck[this.codenum - 1].promotioncol == "<" &&
          this.total <= this.promotioncheck[this.codenum - 1].amont
        ) {
          console.log("1");

          this.total =
            (this.total *
              this.promotioncheck[this.codenum - 1].percentpromotion) /
            100;
        } else {
          await axios
            .put(`http://localhost:3000/canceltPromotion`, {
              cart_id: cartid,
              codepromotion: this.Promotion,
            })
            .then(() => {
              this.checkcode = 0;
              this.Promotion = "";
              this.numcheck = false;
              alert("โค้ด ไม่ตรงตามเงื่อนไข");
            })
            .catch((err) => {
              console.log(err);
            });
        }
      } else {
        alert("โค้ดไม่ถูกต้อง");
        this.Promotion = "";
      }
    },

    async canceltPromotion(cartid) {
      await axios
        .put(`http://localhost:3000/canceltPromotion`, {
          cart_id: cartid,
          codepromotion: this.Promotion,
        })
        .then(() => {
          this.checkcode = 0;
          this.Promotion = "";
          this.total = this.keepnum;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    selectImages(event) {
      this.images = event.target.files;
    },
    async submitpay(cartid) {
      // อันนี้แก้ไขเงินใน cart
      let formData = new FormData();
      formData.append("cart_id", cartid);
      formData.append("price", this.total);
      formData.append("myImage", this.images[0]);
      await axios
        .put(`http://localhost:3000/usedpronotion`, formData)
        .then((response) => {
          this.total = response.data;
          this.numcheck = false;
        })
        .catch((err) => {
          console.log(err);
        });

      await axios
        .post(`http://localhost:3000/addcart`)
        .then(() => {
          window.location.href = "/";
        })
        .catch((error) => {
          this.error = error.response.data.message;
        });
      this.Payment = false;
    },
  },
};
</script>
<style >
@import "~@creativebulma/bulma-divider";
</style>
