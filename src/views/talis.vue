<script setup>

import { ref, onMounted } from 'vue';
import axios from 'axios';

const empList = ref([])

 const search = async () => {
    const result =  await axios.get(`https://web-server.itheima.net/emps/list?name=${emp.value.name}&gender=${emp.value.gender}&job=${emp.value.job}`)
    empList.value = result.data.data

}

const clear = () => {
  emp.value = { name: '', gender: '', job: '' }
  search()
}


const emp = ref({
  name: '',
  gender: '',
  job: '',
})

onMounted(() => {
    emp.value = { name: '', gender: '', job: '' }
    search()
})

</script>

<template>

<div class="container">
    
    <el-form :inline="true" :model="emp" class="demo-form-inline">
            <el-form-item label="姓名">
                <el-input v-model="emp.name" placeholder="请输入姓名" clearable />
            </el-form-item>
            <el-form-item label="性别">
                <el-select
                    v-model="emp.gender"
                    placeholder="请选择性别"
                    clearable
                >
                    <el-option label="男" value="1" />
                    <el-option label="女" value="2" />
                </el-select>
            </el-form-item>
            <el-form-item label="职位">
                <el-select
                    v-model="emp.job"
                    placeholder="请选择职位"
                    clearable
                >
                    <el-option label="班主任" value="1" />
                    <el-option label="讲师" value="2" />
                    <el-option label="学工主管" value="3" />
                    <el-option label="教工主管" value="4" />
                    <el-option label="咨询师" value="5" />
                </el-select>
            </el-form-item>
            <el-form-item>
            <el-button type="primary" @click="search">查询</el-button>
            <el-button type="info" @click="clear">清空</el-button>
            </el-form-item>
        </el-form>

        <el-table :data="empList" :align="center" border style="width: 100%">
            <el-table-column prop="id" label="ID" width="180"  align="center"/>
            <el-table-column prop="name" label="姓名" width="180"  align="center"/>
            <el-table-column label="头像" width="180" align="center" >
                <template #default="scope">
                    <img :src="scope.row.image" width="80px" alt="头像" >
                </template>
            </el-table-column>
            <el-table-column label="性别" width="180"  align="center">
                <template #default="scope">
                    <span v-if="scope.row.gender == 1">男</span>
                    <span v-else>女</span>
                </template>
            </el-table-column>
            <el-table-column label="职位" width="180"  align="center">
                <template #default="scope">
                    <span v-if="scope.row.job == 1">班主任</span>
                    <span v-else-if="scope.row.job == 2">讲师</span>
                    <span v-else-if="scope.row.job == 3">学工主管</span>
                    <span v-else-if="scope.row.job == 4">教工主管</span>
                    <span v-else-if="scope.row.job == 5">咨询师</span>
                    <span v-else>其他</span>
                </template>
            </el-table-column>
            <el-table-column prop="entrydate" label="入职日期" width="180"  align="center"/>
            <el-table-column prop="updatetime" label="更新时间"  align="center"/>
        </el-table>
</div>

</template>

<style scoped>

.container {
    margin: 0 auto;
    width: 70%;
    text-align: center;

}
</style>