<template>
  <div>
    <el-cascader
      v-model="province"
      :options="OPTIONS1"
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
import { deepClone } from '@/utils/index'

export default {
  name: 'CUSTOMADDRESS',
  props: {
    disabled: Boolean,
    size: {
      type: String,
      default: ''
    },
    readonly: Boolean,
    required: {
      type: Boolean,
      default: false
    },
    conf: {
      default: Object
    },
    addressType: {
      type: Number,
      default: 3
    }
  },
  data() {
    return {
      OPTIONS,
      OPTIONS1: [],
      province: '',
      detailAddress: ''
    }
  },
  watch: {
    addressType: {
      immediate: true,
      handler(val) {
        let options = deepClone(OPTIONS)
        if (val === 2) {
          options.forEach(i => {
            i?.children.forEach(city => {
              delete city.children
            })
          })
        } else if (val === 1) {
          options.forEach(i => {
            delete i?.children
          })
        } else {
          options = deepClone(OPTIONS)
        }
        this.OPTIONS1 = deepClone(options)
      }
    }
  },
  methods: {
    handleChange() {
      const addressEmit = {
        province: this.province,
        address: this.detailAddress
      }
      console.log(addressEmit, 1)
      this.$emit('address-change', addressEmit)
    }
  }
}
</script>
