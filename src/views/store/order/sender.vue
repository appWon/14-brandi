<template>
  <div class="container">
    <div class="senderContainer">
      <div class="senderTitle">
        <h2>주문자 정보</h2>
      </div>
      <div class="senderBox">
        <div class="senderWrap">
          <div class="senderInfo">이름</div>
          <div class="contact nameInput">
            <input type="text" class="senderName" placeholder="이름" maxlength="8" v-model="this.senderName"/>
          </div>
        </div>
        <div class="senderWrap">
          <div class="senderInfo">전화번호</div>
          <div class="contact phoneInput">
            <input type="tel" name="phone1" maxlength="3" v-model="phoneNumber1"/>
            <span>-</span>
            <input type="tel" name="phone2" maxlength="4" v-model="phoneNumber2"/>
            <span>-</span>
            <input type="tel" name="phone2" maxlength="4" v-model="phoneNumber3"/>
          </div>
        </div>
        <div class="senderWrap">
          <div class="senderInfo emailInput">이메일</div>
          <div class="contact">
            <input type="text" name="email1" v-model="email[0]"/>
            <span>@</span>
            <input type="text" name="email2" v-model="email[1]"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios"
export default {
  mounted() {
    axios.get("http://192.168.40.114:5000/checkout/sender",  {
        headers: {
          Authorization:"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50X2lkIjoxNTIsInVzZXJuYW1lIjoidGVzdGJyYW5kaSIsInBlcm1pc3Npb25fdHlwZV9pZCI6MywiZXhwIjoxNjA5OTM0MTUxfQ.m7ZAbo1R3s4o80eFUH3XowNKeEJhqDeIyloM3LTzCIg"
            // localStorage.getItem("token")
        }
      }
    )
      .then(res => {
        this.senderName = res.data.result.name;
        this.senderPhone = res.data.result.phone;
        this.senderEmail = res.data.result.email;
      }
      )
  },

data() {
  return {
      senderName: "",
      senderPhone: "",
      senderEmail: "",
    }
    },
  computed: {
    phoneNumber1: function () {
      return this.senderPhone.substring(0,3);
    },
    phoneNumber2: function () {
      return this.senderPhone.substring(3,7);
    },
    phoneNumber3: function () {
      return this.senderPhone.substring(7,12);
    },
    email: function () {
      return this.senderEmail.split("@");
    }
  }
}
</script>

<style lang="scss" scoped>

.senderContainer{
  color: #1e1e1e;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  .senderTitle{
    width: 100%;
    margin: 90px 0 0 0;
    border-bottom: 1px solid #000000;

    h2{
      font-size: 26px;
      font-weight: normal;
    }
  }

  .senderBox{
    &:last-child{border-bottom: 2px solid #000000}
    width: 100%;

    .senderWrap {
      border-bottom: 1px solid #bdbdbd;

      .senderInfo {
        width: 20%;
        font-size: 15.6px;
        font-weight: bold;
        padding: 15px 10px 15px 10px;
        display: inline-block;
      }

      .contact {
        padding: 15px 10px 15px 10px;
        display: inline-block;
      }

      .nameInput{
        width: 75%;

        .senderName{
          width: 100%;
        }
      }

      input {
        background-color: #f5f5f5;
        padding: 13px;
        font-size: 13px;
        border: none;
      }
    }
  }
}
</style>
