<template>
  <form>
    <div v-for="(input, index) in inputArr" class="inputBox" v-bind:key="input.name">
      <div class="user">
        <input
          v-bind:class="isEmailValid(input.name)"
          v-model="inputVal[index]"
          v-on:click="changeInputType(input)"
          v-on:keyup="notifyValue()"
          v-bind:id="input.name"
          autocomplete="false"
          v-bind:type="input.type"
          v-bind:placeholder="input.placeholder"
        >
        <i class="fa fa-envelope fa-lg fa-fw" aria-hidden="true"></i>
        <span class="inputHint">{{input.placeholder}}</span>
        <button id="forgot" v-if="input.type==='password'">Forgot?</button>
      </div>
    </div>
  </form>
</template>

<script>
function getDefaultData() {
  return {
    inputVal: [],
    mailErr: false,
    reg: /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/
  };
}
export default {
  data() {
    return getDefaultData();
  },
  props: {
    inputArr: Array
  },
  methods: {
    changeInputType(type) {
      this.inputArr.forEach(el => {
        el.isSelected = false;
      });
      type.isSelected = true;
    },
    notifyValue() {
      this.$emit("notifyInputChange", this.inputVal, this.mailErr);
    },
    isEmailValid(name) {
      if (name === "email") {
        let email = this.inputVal[0];
        if (email && (this.inputVal[0] !== "" && !this.reg.test(email))) {
          this.mailErr = true;
          return "has-error";
        }
        this.mailErr = false;
        return "";
      }
      return "";
    }
  }
};
</script>

<style scoped>
/* user */
.user {
  position: relative;
  display: inline-block;
  padding-top: 10px;
  margin-top: 15px;
  width: 80%;
  max-width: 300px;
}

.user input {
  text-indent: 20px;
  height: 30px;
  width: 100%;
  border: 1px solid lightgrey;
  border-radius: 4px;
}

.user input:focus {
  outline: none;
  border: 2px solid lightskyblue;
  border-radius: 4px;
}
.user i {
  position: absolute;
  left: 0;
  top: 8px;
  padding: 9px 8px;
  color: #aaa;
  transition: 0.3s;
}
.has-error {
  outline: none;
  border: 2px solid red !important;
  border-radius: 4px;
}

.InputBox {
  position: relative;
}

/* inputHint */
.inputHint {
  position: absolute;
  display: none;
  background-color: lightskyblue;
  padding: 3px;
  left: 10px;
  bottom: 30px;
  border-radius: 4px;
}

input:focus + .inputHint {
  display: block;
}
/* button */
button {
  position: absolute;
  top: 18px;
  right: 5px;
  height: 20px;
  border-width: 0px 0px 0px 1px;
  border-style: solid;
  border-left-color: lightgrey;
  color: dodgerblue;
  background-color: white;
}
button:focus {
  outline: none;
}
button:hover {
  filter: brightness(1.1);
  cursor: pointer;
}
</style>
