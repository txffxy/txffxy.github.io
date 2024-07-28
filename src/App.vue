<template>
  <main>
    <h1 class="text-center">Chiness Fortune Telling</h1>
    <h2 class="text-center">Said boe Fortune-telling,Prediction of your life</h2>
    <el-divider />
    <el-form
      v-if="!showResultRef"
      class="form"
      ref="formRef"
      :model="form"
      :rules="rules"
      label-width="auto"
      status-icon
    >
      <el-form-item label="Date of Birth" prop="date1">
        <el-date-picker v-model="form.date1" type="date" placeholder="Pick a date" />
      </el-form-item>
      <el-form-item label="Time" prop="date2">
        <div class="form-item-wrap">
          <el-time-picker
            is-range
            v-model="form.date2"
            start-placeholder="Start time"
            end-placeholder="End time"
            style="width: 200px"
          />
        </div>
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
    <template v-else>
      <h3>Information</h3>
      <div class="form">
        <div class="result-item">
          <p class="result-item-label">Chinese calendar:</p>
          <p>{{ format(form.date1, 'yyyy/MM/dd') }}</p>
        </div>
        <div class="result-item">
          <p class="result-item-label">Time:</p>
          <p>{{ format(form.date2[0], 'HH:mm') }}~{{ format(form.date2[1], 'HH:mm') }}</p>
        </div>
        <div class="result-item">
          <p class="result-item-label">Gender:</p>
          <p>{{ form.gender }}</p>
        </div>
      </div>
      <el-divider />
      <h3>Result</h3>
      <div class="form">
        <div class="result-item">
          <p class="result-item-label">weight:</p>
          <p>{{ result.weight }}</p>
        </div>
        <div class="result-item">
          <p class="result-item-label">key word:</p>
          <div>{{ result.keyWord }}</div>
        </div>
        <div class="result-item">
          <p class="result-item-label">translation:</p>
          <p>{{ result.translation }}</p>
        </div>
      </div>
    </template>
  </main>
</template>

<script lang="ts" setup>
import { reactive, ref } from 'vue'
import { format } from 'date-fns'
const formRef = ref()
const form = reactive({
  date1: '',
  date2: '',
  gender: ''
})

const rules = reactive({
  date1: [
    {
      required: true,
      message: 'Please pick a date',
      trigger: 'change'
    }
  ],
  date2: [
    {
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

const showResultRef = ref(false)

const result = reactive({
  weight: '3.8',
  keyWord: '奥斯丁发射点法上的发生的发生的发生的发射点法沙发上',
  translation:
    'asdfasdfasf1sef asdfa sdfasdf asdf asdf asdf2r134 sfsdsd sdf;klsj ks askdjflksjdfoiwjfknssd skdjf '
})

const handleSubmit = async (formEl) => {
  console.log('handleSubmit', form)
  await formEl.validate((valid, fields) => {
    if (valid) {
      console.log('submit!')
      showResultRef.value = true
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
}
.text-center {
  text-align: center;
}
.form {
  max-width: 600px;
  margin: 0 auto;
}
.result-item {
  margin-top: 8px;
  display: flex;
}
.result-item-label {
  margin-right: 8px;
}
</style>
