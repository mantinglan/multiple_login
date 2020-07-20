<template>
  <div id="app">
    <div class="header">
      <span>Choose Account Type</span>
    </div>
    <AccountType v-bind:typeArr="accountTypeArr" v-on:notifyTypeChange="typeChange"/>
    <div class="greeting">
      <span>
        Hello {{this.currentType}} !
        <br>Please fill out the form to get started
      </span>
    </div>
    <div>
      <InputBox v-bind:inputArr="inputArr" v-on:notifyInputChange="inputChange"/>
      <div class="form__bottom">
        <div class="footer">
          <span>No Account?</span>
          <button class="signBtn" v-on:click="signUp()">Signup</button>
        </div>
        <div class="footer">
          <button class="loginBtn" v-on:click="checkInput()" v-bind:class="buttonDisable()">Login</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
import InputBox from "./components/InputBox";
import AccountType from "./components/AccountType";
import doctorSVG from "./assets/img_doctor.svg";
import patientSVG from "./assets/img_patient.svg";
const searchTerm = "@";

export default {
  name: "App",
  data() {
    return {
      doctorSVG,
      patientSVG,
      accountTypeArr: [
        { name: "Doctor", typeSrc: doctorSVG, isSelected: true },
        { name: "Patient", typeSrc: patientSVG, isSelected: false }
      ],
      inputArr: [
        {
          name: "email",
          type: "email",
          placeholder: "Email",
          isSelected: true
        },
        {
          name: "password",
          type: "password",
          placeholder: "Password",
          isSelected: false
        }
      ],
      currentType: "doctor",
      currentName: "",
      currentPsw: "",
      inputErr: false,
      pswHint:
        "Any consecutive 6 digits of the password cannot be repeated with any consecutive 6 digits of the username.",
      emptyHint: "The user name or password can't be empty."
    };
  },
  methods: {
    typeChange(type) {
      this.currentType = type.toLowerCase();
    },
    inputChange(Entry, mailErr) {
      this.currentName = Entry[0];
      this.currentPsw = Entry[1];
      this.inputErr = mailErr;
    },
    checkInput() {
      if (this.currentName === "" || this.currentPsw === "") {
        return alert(this.emptyHint);
      }
      let userName = this.currentName.substring(
        0,
        this.currentName.indexOf(searchTerm)
      );
      if (userName === this.currentPsw) {
        return alert(this.pswHint);
      }
      if (this.currentPsw.length > 6) {
        for (let i = 0; i <= this.currentPsw.length - 6; i++) {
          if (userName.indexOf(this.currentPsw.slice(i, i + 6)) !== -1)
            return alert(this.pswHint);
        }
        return alert("Login success!");
      } else {
        if (userName.indexOf(this.currentPsw) !== -1) {
          return alert(this.pswHint);
        }
      }
    },
    signUp() {
      alert("Sign up");
    },
    buttonDisable() {
      return this.inputErr === true ? "buttonDisable disabled" : "";
    }
  },
  components: {
    HelloWorld,
    InputBox,
    AccountType
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 12px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  height: 100vh;
}
body {
  background-image: url(img_town.svg);
  background-repeat: no-repeat;
  background-position: bottom;
  background-size: contain;
}
.header {
  color: dodgerblue;
  padding-top: 10vh;
}
.greeting {
  margin: 20px;
  color: lightgrey;
}
.loginBtn {
  background-color: dodgerblue;
  border: none;
  color: white;
  width: 100px;
  height: 30px;
  text-align: center;
  font-size: 14px;
  border-radius: 4px;
  margin-top: 10px;
}
.loginBtn:hover {
  filter: brightness(1.1);
  color: white;
  cursor: pointer;
}
.signBtn {
  color: dodgerblue;
  background-color: white;
  border: none;
}
.signBtn:hover {
  filter: brightness(1.1);
  cursor: pointer;
}
.form__bottom {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 10px;
  flex-wrap: wrap;
}
.footer {
  margin: 15px;
}
button:focus {
  outline: none;
}
button:hover {
  cursor: pointer;
}
.buttonDisable {
  opacity: 0.4;
  box-shadow: 0 1px 0 rgba(35, 35, 35, 0.2);
  cursor: not-allowed !important;
}
</style>
