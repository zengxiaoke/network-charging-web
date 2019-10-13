<template>
  <div>
    <p>
      <el-button @click="showAdd = true">Add</el-button>
    </p>
    <el-table :data="tblData">
      <el-table-column prop="buildingCode" label="building code"></el-table-column>
      <el-table-column prop="roomCode" label="room code"></el-table-column>
      <el-table-column prop="personName" label="person name"></el-table-column>
      <el-table-column prop="phoneNum" label="Phone Num"></el-table-column>
      <el-table-column prop="fromDate" label="from date"></el-table-column>
      <el-table-column prop="toDate" label="to code"></el-table-column>
      <el-table-column fixed="right" label="Operations">
        <template scope="row">
          <el-button>edit</el-button>
        </template>
      </el-table-column>
    </el-table>

    <el-dialog title="Add" :visible.sync="showAdd">
      <el-form :model="addForm" label-width="200px">
        <el-form-item label="building code">
          <el-input v-model="addForm.buildingCode"></el-input>
        </el-form-item>
        <el-form-item label="room code">
          <el-input v-model="addForm.roomCode"></el-input>
        </el-form-item>
        <el-form-item label="person name">
          <el-input v-model="addForm.personName"></el-input>
        </el-form-item>
        <el-form-item label="phone num">
          <el-input v-model="addForm.phoneNum"></el-input>
        </el-form-item>
        <el-form-item label="date range">
          <el-date-picker
            v-model="addForm.fromDate"
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
  </div>
</template>

<script>
export default {
  data() {
    return {
      tblData: [
        {
          buildingCode: "#4",
          roomCode: "001",
          phoneNum: "001",
          personName: "ali",
          fromDate: "2010-1-1",
          toDate: "2010-3-3"
        }
      ],
      showAdd: false,
      addForm: {
        buildingCode: "#4",
        roomCode: "001",
        phoneNum: "001",
        personName: "ali",
        fromDate: "2010-1-1",
        toDate: "2010-3-3"
      }
    };
  }
};
</script>

<style>
</style>
