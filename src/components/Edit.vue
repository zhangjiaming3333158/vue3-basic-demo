<script setup>
// TODO: 编辑
import { ref } from 'vue'
import axios from 'axios'
// 弹框开关
const dialogVisible = ref(false)

// form
const form = ref({
  name: '',
  place: '',
  id: ''
})

//open dialog
const open = (item) => {
  dialogVisible.value = true
  form.value.name = item.name
  form.value.place = item.place
  form.value.id = item.id
}

//emit
const emit = defineEmits(['update-list'])
const emitForm = async () => {
  await axios.patch(`/edit/${form.value.id}`, form.value)
  dialogVisible.value = false
  emit('update-list')
}


//宏定义
defineExpose({
  open
})
</script>

<template>
  <el-dialog v-model="dialogVisible" title="编辑" width="400px">
    <el-form label-width="50px">
      <el-form-item label="姓名">
        <el-input placeholder="请输入姓名" v-model="form.name" />
      </el-form-item>
      <el-form-item label="籍贯">
        <el-input placeholder="请输入籍贯" v-model="form.place"/>
      </el-form-item>
    </el-form>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogVisible = false">取消</el-button>
        <el-button type="primary" @click="emitForm">确认</el-button>
      </span>
    </template>
  </el-dialog>
</template>

<style scoped>
.el-input {
  width: 290px;
}
</style>
