<template>
  <main>
    <h1>Chiness Fortune Telling</h1>
    <h2>Said boe Fortune-telling,Prediction of your life</h2>
    <el-divider />
    <el-form ref="formRef" :model="form" :rules="rules" label-width="auto" status-icon>
      <el-form-item label="Date of Birth" prop="date1">
        <el-date-picker v-model="form.date1" type="date" placeholder="Pick a date" />
      </el-form-item>
      <el-form-item label="Time" prop="date2">
        <el-time-picker v-model="form.date2" placeholder="Pick a time" />
      </el-form-item>
      <el-form-item label="Gender" prop="gender">
        <el-radio-group v-model="form.gender">
          <el-radio value="Male">Male</el-radio>
          <el-radio value="Female">Female</el-radio>
        </el-radio-group>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="handleSubmit(formRef)">GET YOUT ANSWER</el-button>
      </el-form-item>
    </el-form>
  </main>
</template>

<script lang="ts" setup>
import { reactive, ref } from 'vue'

const formRef = ref()
const form = reactive({
  date1: '',
  date2: '',
  gender: ''
})

const rules = reactive({
  date1: [
    {
      type: 'date',
      required: true,
      message: 'Please pick a date',
      trigger: 'change'
    }
  ],
  date2: [
    {
      type: 'date',
      required: true,
      message: 'Please pick a time',
      trigger: 'change'
    }
  ],
  gender: [
    {
      required: true,
      message: 'Please select gender',
      trigger: 'change'
    }
  ]
})

const handleSubmit = async (formEl) => {
  console.log('handleSubmit', form)
  await formEl.validate((valid, fields) => {
    if (valid) {
      console.log('submit!')
    } else {
      console.log('error submit!', fields)
    }
  })
}
</script>
<style scoped>
main {
  margin: 0 auto;
  max-width: 800px;
  text-align: center;
}
</style>
