<template>
  <el-dialog title="开通/续费" visible>
    <el-form :model="formModel" label-width="200px">
      <el-form-item label="房号">
        <el-select v-model="formModel.roomCode"></el-select>
      </el-form-item>
      <el-form-item label="楼号">
        <el-input v-model="formModel.buildingCode" disabled></el-input>
      </el-form-item>
      <el-form-item label="住户姓名">
        <el-select v-model="formModel.personName"></el-select>
      </el-form-item>
      <el-form-item label="联系电话">
        <el-input v-model="formModel.phoneNum" disabled></el-input>
      </el-form-item>
      <el-form-item label="网络使用时间">
        <el-date-picker
          v-model="formModel.fromDate"
          type="daterange"
          range-separator="至"
          start-placeholder="开始日期"
          end-placeholder="结束日期"
        ></el-date-picker>
      </el-form-item>
    </el-form>

    <template slot="footer">
      <el-button type="primary">Confirm</el-button>
      <el-button>Cancel</el-button>
    </template>
  </el-dialog>
</template>

<script>
export default {
  data() {
    return {
      formModel: {
        roomCode: "001",
        buildingCode: "#4",
        personName: "ali",
        phoneNum: "001",
        fromDate: "2010-1-1",
        toDate: "2010-3-3",
        creator: "9527"
      }
    };
  }
};
</script>

<style>
</style>
