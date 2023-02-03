<template>
  <div class="main">
    <Form
      ref="form"
      :data-items="state.dataItem"
      label-width="auto"
      :form-data="state.formData"
      :rules="state.validateForm"
    />
  </div>
</template>
<script setup lang='ts'>
import Form from './MyForm/Form.vue'
import  validateRules  from "./MyForm/formValidate";
import { reactive, ref } from 'vue';
// 表单数据以及校验
const state = reactive({
    formData: {
        name: '',
        description: ''
        // password: ''
    },
    dataItem: [
      {id: 'name', itemType: 'input', place: 'IP校验', label: 'IP'},
      {id: 'description', itemType: 'input', place: '长度校验，最多8位', label: '长度校验：'}
    ],
    validateForm: {
        name: [
            {
                validator: validateRules,
                  required: true,
                rules: {
                  required: true,
                  length: [1,16],
                  reg: 'IP',
                },
                trigger: 'blur',
                  label:'IP'
            }
        ],
        description: [
            {
                validator: validateRules,
                  required: true,
                rules: {
                  required: true,
                  length: [1,16],
                },
                trigger: 'blur',
                  label:'长度校验'
            }
        ]
    }
})

</script>
<style lang='css' scoped>
.main{
  width: 460px;
}
</style>