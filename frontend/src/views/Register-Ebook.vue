<template>
  <div>
    <NavBar />

    <div>
      <section class="section">
        <div class="container">
          <div class="columns is-centered">
            <div class="column is-half">
              <div
                class="card column mt-6"
                style="
                  background: linear-gradient(221deg, #edc7b7, #eee2dc 73%);
                "
              >
                <div class="field">
                  <p
                    class="label is-size-4"
                    style="color: #123c69; text-align: center"
                  >
                    <span
                      class="material-icons"
                      style="color: #123c69; text-align: center"
                    >
                      &#xe174;
                    </span>
                    <br />
                    สมัครสมาชิก
                  </p>
                </div>

                <div class="field">
                  <label class="label" style="color: #ac3b61">ชื่อผู้ใช้</label>
                  <div class="control has-icons-left has-icons-right">
                    <input
                      class="input is-medium is-rounded"
                      type="text"
                      style="background-color: #eee2dc"
                      v-model="username"
                    />
                    <span class="icon is-small is-left">
                      <i class="fas fa-user"></i>
                    </span>
                  </div>

                </div>

                <div class="field-body">
                  <div class="field">
                    <div class="control">
                      <label class="label" style="color: #ac3b61"
                        >ชื่อจริง
                      </label>
                      <input
                        class="input is-medium is-rounded"
                        type="text"
                        v-model="first_name"
                        style="background-color: #eee2dc"
                      />
                    </div>
                  </div>
                  <div class="field">
                    <div class="control">
                      <label class="label" style="color: #ac3b61"
                        >นามสกุล
                      </label>
                      <input
                        class="input is-medium is-rounded"
                        type="text"
                        v-model="last_name"
                        style="background-color: #eee2dc"
                      />
                    </div>
                  </div>
                </div>

                <div class="field">
                  <label class="label" style="color: #ac3b61">อีเมล</label>
                  <div class="control has-icons-left has-icons-right">
                    <input
                      class="input is-medium is-rounded"
                      type="email"
                      v-model="email"
                      style="background-color: #eee2dc"
                    />
                    <span class="icon is-small is-left">
                      <i class="fas fa-envelope"></i>
                    </span>
                  </div>
                </div>

                <div class="field-body">
                  <div class="field">
                    <div class="control">
                      <label class="label" style="color: #ac3b61"
                        >วันเกิด</label
                      >
                      <input
                        class="input is-medium is-rounded"
                        type="date"
                        v-model="birthday"
                        style="background-color: #eee2dc"
                      />
                    </div>
                  </div>

                  <div class="field">
                    <label class="label" style="color: #ac3b61">เพศ</label>

                    <div class="select is-fullwidth is-medium is-rounded">
                      <select v-model="sex" style="background-color: #eee2dc">
                        <option value="Male">ชาย</option>
                        <option value="Famale">หญิง</option>
                        <option value="not_specified">ไม่ระบุ</option>
                      </select>
                    </div>
                  </div>
                </div>

                <div class="field">
                  <label class="label" style="color: #123c69"
                    >เบอร์โทรสับ</label
                  >
                  <input
                    :disabled="disabled"
                    class="input is-medium is-rounded"
                    type="text"
                    v-model="mobile"
                    style="background-color: #eee2dc"
                  />
                </div>

                <div class="field-body">
                  <div class="field">
                    <label class="label" style="color: #123c69"
                      >เลขที่บัญชี</label
                    >
                    <input
                      :disabled="disabled"
                      class="input is-medium is-rounded"
                      type="text"
                      v-model="bankName"
                      style="background-color: #eee2dc"
                    />
                  </div>

                  <div class="field">
                    <label class="label" style="color: #123c69"
                      >ชื่อธนาคาร</label
                    >
                    <input
                      :disabled="disabled"
                      class="input is-medium is-rounded"
                      type="text"
                      v-model="bankNumber"
                      style="background-color: #eee2dc"
                    />
                  </div>
                </div>

                <div class="field">
                  <label class="label" style="color: #ac3b61">รหัสผ่าน</label>
                  <input
                    class="input is-medium is-rounded"
                    type="text"
                    v-model="password"
                    style="background-color: #eee2dc"
                  />
                </div>

                <div class="field">
                  <label class="label" style="color: #ac3b61"
                    >ยืนยัน รหัสผ่าน</label
                  >
                  <input
                    class="input is-medium is-rounded"
                    type="text"
                    v-model="confirm_password"
                    style="background-color: #eee2dc"
                  />
                </div>

                <div class="field column">
                  <div class="control">
                    <button
                      class="button"
                      style="color: #eee2dc; background-color: #ac3b61"
                      @click="submit()"
                    >
                      ส่งข้อมูล
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>
<script>
import axios from "@/plugins/axios";
import {
  required,
  email,
  helpers,
  minLength,
  maxLength,
  sameAs,
} from "vuelidate/lib/validators";

function mobile(value) {
  return !helpers.req(value) || !!value.match(/0[0-9]{9}/);
}

function complexPassword(value) {
  if (!(value.match(/[a-z]/) && value.match(/[A-Z]/) && value.match(/[0-9]/))) {
    return false;
  }
  return true;
}

export default {
  data() {
    return {
      username: "",
      password: "",
      confirm_password: "",
      email: "",
      mobile: "",
      first_name: "",
      last_name: "",
      sex: "",
      birthday: ""
    };
  },
  methods: {
    submit() {

        let data = {
          username: this.username,
          password: this.password,
          sex: this.sex,
          birthdate: this.birthday,
          email: this.email,
          mobile: this.mobile,
          first_name: this.first_name,
          last_name: this.last_name,
        };

        axios
          .post("http://localhost:3000/user/signup", data)
          .then(() => {
            alert("Sign up Success");
          })
          .catch((err) => {
            alert(err.response.data.details);
          });
      
    },
  },
  validations: {
    email: {
      required: required,
      email: email,
    },
    mobile: {
      required: required,
      mobile: mobile,
    },
    password: {
      required: required,
      minLength: minLength(8),
      complex: complexPassword,
    },
    confirm_password: {
      sameAs: sameAs("password"),
    },
    username: {
      required: required,
      minLength: minLength(5),
      maxLength: maxLength(20),
    },
    first_name: {
      required: required,
    },
    last_name: {
      required: required,
    },
  },
};
</script>
<style lang="">
</style>
