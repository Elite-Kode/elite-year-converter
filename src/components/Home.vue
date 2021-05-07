<template>
  <div class="d-flex flex-column" style="height: 100%" v-resize="onResize">
    <div class="flex-grow-1 primary d-flex justify-center" ref="top">
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        :style="{ width: width + 'px' }"
      ></v-text-field>
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        :style="{ width: width + 'px' }"
      ></v-text-field>
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        :style="{ width: width + 'px' }"
      ></v-text-field>
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        :style="{ width: width + 'px' }"
      ></v-text-field>
    </div>
    <div class="flex-grow-1 secondary d-flex justify-center" ref="bottom">
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        :style="{ width: width + 'px' }"
      ></v-text-field>
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        :style="{ width: width + 'px' }"
      ></v-text-field>
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        :style="{ width: width + 'px' }"
      ></v-text-field>
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        :style="{ width: width + 'px' }"
      ></v-text-field>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      width: 0
    }
  },
  mounted() {
    this.onResize()
  },
  methods: {
    onResize() {
      let windowHeight = window.innerHeight / 2
      let fontSize = windowHeight * 0.6
      this.width = fontSize / 1.3
      if ((this.width + 16) * 4 > this.$refs.top.clientWidth) {
        this.width = this.$refs.top.clientWidth / 4 - 16
        fontSize = this.width * 1.3
      }

      this.$refs.top.children.forEach((child) => {
        child.children[0].children[0].style = `width: ${this.width}px !important`
        child.children[0].children[0].children[1].children[0].style = `font-size: ${fontSize}px !important`
      })

      this.$refs.bottom.children.forEach((child) => {
        child.children[0].children[0].style = `width: ${this.width}px !important`
        child.children[0].children[0].children[1].children[0].style = `font-size: ${fontSize}px !important`
      })
    }
  }
}
</script>

<style>
.v-input__control {
  height: 100%;
}

.v-input__slot {
  height: 100%;
  margin-top: 8px;
}

input {
  max-height: 100% !important;
  text-align: center;
  caret-color: transparent;
}

.v-text-field__details {
  display: none !important;
}
</style>
