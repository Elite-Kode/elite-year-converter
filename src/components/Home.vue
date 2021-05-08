<template>
  <div class="d-flex flex-column" style="height: 100%" v-resize="onResize">
    <div class="flex-grow-1 primary d-flex justify-center" ref="top">
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        autofocus
        v-model="field0"
        :style="{ width: width + 'px' }"
      ></v-text-field>
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        v-model="field1"
        :style="{ width: width + 'px' }"
      ></v-text-field>
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        v-model="field2"
        :style="{ width: width + 'px' }"
      ></v-text-field>
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        v-model="field3"
        :style="{ width: width + 'px' }"
      ></v-text-field>
    </div>
    <div class="flex-grow-1 accent d-flex justify-center" ref="bottom">
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        v-model="field4"
        :style="{ width: width + 'px' }"
      ></v-text-field>
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        v-model="field5"
        :style="{ width: width + 'px' }"
      ></v-text-field>
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        v-model="field6"
        :style="{ width: width + 'px' }"
      ></v-text-field>
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
        v-model="field7"
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
      width: 0,
      eliteYear: 0,
      localYear: 0,
      field0: '',
      field1: '',
      field2: '',
      field3: '',
      field4: '',
      field5: '',
      field6: '',
      field7: ''
    }
  },
  created() {
    this.field0 = new Date().getFullYear().toString().slice(0, 1)
    this.field1 = new Date().getFullYear().toString().slice(1, 2)
    this.field2 = new Date().getFullYear().toString().slice(2, 3)
    this.field3 = new Date().getFullYear().toString().slice(3, 4)
  },
  mounted() {
    this.onResize()
  },
  watch: {
    field0() {
      this.checkTopFieldEntry()
    },
    field1() {
      this.checkTopFieldEntry()
    },
    field2() {
      this.checkTopFieldEntry()
    },
    field3() {
      this.checkTopFieldEntry()
    },
    field4() {
      this.checkBottomFieldEntry()
    },
    field5() {
      this.checkBottomFieldEntry()
    },
    field6() {
      this.checkBottomFieldEntry()
    },
    field7() {
      this.checkBottomFieldEntry()
    },
    eliteYear() {
      this.field4 = this.eliteYear.toString().slice(0, 1)
      this.field5 = this.eliteYear.toString().slice(1, 2)
      this.field6 = this.eliteYear.toString().slice(2, 3)
      this.field7 = this.eliteYear.toString().slice(3, 4)
    },
    localYear() {
      this.field0 = this.localYear.toString().slice(0, 1)
      this.field1 = this.localYear.toString().slice(1, 2)
      this.field2 = this.localYear.toString().slice(2, 3)
      this.field3 = this.localYear.toString().slice(3, 4)
    }
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

      this.$refs.top.children.forEach((child, index) => {
        child.children[0].children[0].style = `width: ${this.width}px !important`
        child.children[0].children[0].children[1].children[0].style = `font-size: ${fontSize}px !important`
        child.children[0].children[0].children[1].children[0].maxLength = 1
        child.children[0].children[0].children[1].children[0].addEventListener('keypress', (event) => {
          if (!isNaN(event.key)) {
            this[`field${index}`] = event.key
          }
        })
      })

      this.$refs.bottom.children.forEach((child, index) => {
        child.children[0].children[0].style = `width: ${this.width}px !important`
        child.children[0].children[0].children[1].children[0].style = `font-size: ${fontSize}px !important`
        child.children[0].children[0].children[1].children[0].maxLength = 1
        child.children[0].children[0].children[1].children[0].addEventListener('keypress', (event) => {
          if (!isNaN(event.key)) {
            this[`field${index + 4}`] = event.key
          }
        })
      })
    },
    checkTopFieldEntry() {
      if (this.field0 && this.field1 && this.field2 && this.field3) {
        this.eliteYear = parseInt(this.field0 + this.field1 + this.field2 + this.field3) + 1286
      }
    },
    checkBottomFieldEntry() {
      if (this.field4 && this.field5 && this.field6 && this.field7) {
        this.localYear = parseInt(this.field4 + this.field5 + this.field6 + this.field7) - 1286
      }
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
