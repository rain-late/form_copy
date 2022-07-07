<template>
  <div>
    <el-cascader
      v-model="province"
      :options="OPTIONS"
      :disabled="disabled"
      :readonly="readonly"
      :required="required"
      @change="handleChange"
    />

    <el-input
      v-model="detailAddress"
      :disabled="disabled"
      :readonly="readonly"
      :required="required"
      style="margin-top: 10px"
      @blur="handleChange"
    />
  </div>
</template>

<script>
import OPTIONS from '../../generator/province.js'

export default {
  name: 'CUSTOMADDRESS',
  props: {
    disabled: Boolean,
    size: {
      type: String,
      default: ''
    },
    readonly: Boolean,
    // province: {
    //   type: Object,
    //   default: null
    // },
    // detailAddress: {
    //   type: Object,
    //   default: null
    // },
    required: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      OPTIONS,
      province: '',
      detailAddress: ''
    }
  },
  methods: {
    handleChange() {
      const addressEmit = {
        province: this.province,
        address: this.detailAddress
      }
      console.log(addressEmit)
      this.$emit('address-change', addressEmit)
    }
  }
}
</script>
