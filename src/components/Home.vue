<template>
  <div class="d-flex flex-column" style="height: 100%" v-resize="onResize">
    <div class="flex-grow-1 primary d-flex justify-center" ref="top">
      <v-text-field
        class="align-center flex-grow-0 mx-2"
        color="white"
        outlined
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
    <div class="flex-grow-1 secondary d-flex justify-center" ref="bottom">
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
    field0(newValue, oldValue) {
      this.checkTopFieldEntry(0, newValue, oldValue)
    },
    field1(newValue, oldValue) {
      this.checkTopFieldEntry(1, newValue, oldValue)
    },
    field2(newValue, oldValue) {
      this.checkTopFieldEntry(2, newValue, oldValue)
    },
    field3(newValue, oldValue) {
      this.checkTopFieldEntry(3, newValue, oldValue)
    },
    field4(newValue, oldValue) {
      this.checkBottomFieldEntry(4, newValue, oldValue)
    },
    field5(newValue, oldValue) {
      this.checkBottomFieldEntry(5, newValue, oldValue)
    },
    field6(newValue, oldValue) {
      this.checkBottomFieldEntry(6, newValue, oldValue)
    },
    field7(newValue, oldValue) {
      this.checkBottomFieldEntry(7, newValue, oldValue)
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

      this.$refs.top.children.forEach((child) => {
        child.children[0].children[0].style = `width: ${this.width}px !important`
        child.children[0].children[0].children[1].children[0].style = `font-size: ${fontSize}px !important`
      })

      this.$refs.bottom.children.forEach((child) => {
        child.children[0].children[0].style = `width: ${this.width}px !important`
        child.children[0].children[0].children[1].children[0].style = `font-size: ${fontSize}px !important`
      })
    },
    checkTopFieldEntry(fieldIndex, newValue, oldValue) {
      if (newValue.length === 2 && newValue.includes(oldValue)) {
        this[`field${fieldIndex}`] = newValue.replace(oldValue, '')
      } else {
        this[`field${fieldIndex}`] = newValue.substr(newValue.length - 1, 1)
      }
      if (this.field0 && this.field1 && this.field2 && this.field3) {
        this.eliteYear = parseInt(this.field0 + this.field1 + this.field2 + this.field3) + 1286
      }
    },
    checkBottomFieldEntry(fieldIndex, newValue, oldValue) {
      if (newValue.length === 2 && newValue.includes(oldValue)) {
        this[`field${fieldIndex}`] = newValue.replace(oldValue, '')
      } else {
        this[`field${fieldIndex}`] = newValue.substr(newValue.length - 1, 1)
      }
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
