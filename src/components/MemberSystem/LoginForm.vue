<template>
<div  class="row justify-content-center align-items-center vh-100">
  <div class="card text-center w-50">
      <h5 class="card-header">
        會員登入
      </h5>
      <div class="card-body">
        <form  @submit.prevent="signin">
          <div class="list-group list-group-flush">
            <div class="form-floating row justify-content-center mb-3">
              <input class="form-control w-75 "
              placeholder="name@example.com"
              v-model="user.user_id"
              >
              <label for="floatingInput">Email帳號</label>
            </div>


            <div class="form-floating row justify-content-center  mb-3">
              <input type="password"
              class="form-control w-75 "
              placeholder="Password"
              v-model="user.password"
              >
              <label for="floatingPassword">Password</label>
            </div>
         </div>
            <div class="card-footer">
              <input type="submit" class="btn btn-primary" value="Submit">
            </div>
          </form>
      </div>
    </div>
  </div>

</template>

<script>
import {setCookies} from "@/tools/cookies";
import axios from "axios";
export default {
  name: 'LoginForm',
  data () {
    return {
      user: {
        user_id: '',
        password: ''
      }
    }
  },
  methods: {
    signin () {
      let re = ".com"
      const token = 'asds32adsavrAS3Fadf5567'
      const user_id = this.user.user_id
      const password = this.user.password
      if (user_id.search(re) > 0) {
        axios.post(process.env.VUE_APP_LOGIN, {
          user_id: user_id,
          password: password
        }).then((res) => {
          if (res.data.message === '登入成功') {
            const username = res.data.username
            const login_cookie = {user_id,password,username,token}
            setCookies('login',login_cookie)
            this.$router.push({name: 'Admin'})
          }
        },(reject) =>{
          console.log(reject);
        })
      } else {
        alert('格式不合規定')
      }
    },
  }
}
</script>