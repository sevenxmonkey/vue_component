<template>
  <div class="wrapper">
    <div class="container">
      <div class="input-item">
        <input
          id="input-before"
          name="input-before"
          v-model="inchUnit"
          @input="onChangeInput(0)"
        />
        <label for="input-before">Inch</label>
        
      </div>
      <span>=</span>
      <div class="input-item">
        <input
          id="input-after"
          name="input-after"
          v-model="millimeterUnit"
          @input="onChangeInput(1)"
        />
        <label for="input-after">millimeter</label>
      </div>
    </div>
    <div class="warning" v-if="warning">Input must be a number!</div>
  </div>
</template>

<script>
export default {
  name: "UnitConverter",
  data() {
    return {
      inchUnit: 0,
      millimeterUnit: 0,
      warning: false,
    };
  },
  methods: {
    onChangeInput(index) {
        this.warning = false;
      if (index === 0) {
        if (!this.validate(this.inchUnit)) {
          this.millimeterUnit = "";
          this.renderWarning();
          return;
        }
        this.millimeterUnit = (this.inchUnit * 25.4).toFixed(3);
      } else if (index === 1) {
        if (!this.validate(this.millimeterUnit)) {
          this.inchUnit = "";
          this.renderWarning();
          return;
        }
        this.inchUnit = (this.millimeterUnit / 25.4).toFixed(3);
      }
    },
    validate(input) {
      return !isNaN(Number(input));
    },
    renderWarning() {
        this.warning = true;
    },
  },
};
</script>

<style scoped>
input {
  margin: 0 10px;
}
.container {
  display: flex;
  margin: 20px;
}
.input-item {
  margin: 0 10px;
}
.warning{
    color: red;
}
</style>