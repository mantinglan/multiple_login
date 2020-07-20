<template>
  <div class="row">
    <div
      v-bind:class="type.isSelected ? 'col isSelected' : 'col'"
      v-on:click="changeType(type)"
      v-for="type in typeArr"
      v-bind:key="type.name"
    >
      <div class="typePic">
        <span v-html="type.typeSrc"></span>
      </div>
      <div class="bottom">
        <div class="intro">{{type.name}}</div>
        <div class="picture" v-show="type.isSelected">
          <span v-html="selectedSVG"></span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import selectedSVG from "../assets/selected.svg";

function getDefaultData() {
  return {
    selectedSVG,
    currentType: "doctor"
  };
}

export default {
  data() {
    return getDefaultData();
  },
  props: {
    typeArr: Array
  },
  methods: {
    changeType(type) {
      this.$emit("notifyTypeChange", type.name);
      this.typeArr.forEach(ele => {
        ele.isSelected = false;
      });
      type.isSelected = true;
    }
  }
};
</script>

<style scoped>
.row {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
.col {
  width: 120px;
  margin: 20px;
  cursor: pointer;
  border-radius: 4px;
}
.isSelected {
  border: solid rgb(117, 227, 235) 1.5px;
}
.button {
  position: relative;
}
.picture {
  position: relative;
  float: right;
  top: 15px;
  left: 58px;
  width: 100%;
}
.picture img {
  width: 100%;
}
</style>
