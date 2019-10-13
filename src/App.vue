<template>
  <div>
    <p>
      <el-button @click="onAdd">新开通</el-button>
    </p>
    <el-table :data="tblData">
      <el-table-column label="序号" type="index" :index="1"></el-table-column>
      <el-table-column prop="buildingCode" label="楼号"></el-table-column>
      <el-table-column prop="roomCode" label="房号"></el-table-column>
      <el-table-column prop="personName" label="住户姓名"></el-table-column>
      <el-table-column prop="phoneNum" label="联系电话"></el-table-column>
      <el-table-column prop="dateRange[0]" label="开通/续费时间"></el-table-column>
      <el-table-column prop="dateRange[1]" label="到期时间"></el-table-column>
      <el-table-column prop="creator" label="录入人"></el-table-column>
      <el-table-column fixed="right" label="Operations">
        <template scope="row">
          <el-button>修改</el-button>
        </template>
      </el-table-column>
    </el-table>

    <el-dialog title="新开通" :visible.sync="showAdd">
      <el-form :model="addForm" label-width="200px">
        <el-form-item label="楼号">
          <el-input v-model="addForm.buildingCode"></el-input>
        </el-form-item>
        <el-form-item label="房号">
          <el-input v-model="addForm.roomCode"></el-input>
        </el-form-item>
        <el-form-item label="住户姓名">
          <el-input v-model="addForm.personName"></el-input>
        </el-form-item>
        <el-form-item label="联系电话">
          <el-input v-model="addForm.phoneNum"></el-input>
        </el-form-item>
        <el-form-item label="网络使用时间">
          <el-date-picker
            v-model="addForm.dateRange"
            type="daterange"
            range-separator="至"
            start-placeholder="开始日期"
            end-placeholder="结束日期"
            value-format="yyyy-MM-dd"
          ></el-date-picker>
        </el-form-item>
        <el-form-item label="录入人">
          <el-input v-model="addForm.creator"></el-input>
        </el-form-item>
      </el-form>

      <template slot="footer">
        <el-button type="primary" @click="onConfirm">确认</el-button>
        <el-button @click="onCancel">取消</el-button>
      </template>
    </el-dialog>

    <!-- <renewing-form-dialog></renewing-form-dialog> -->
  </div>
</template>

<script>
import RenewingFormDialog from "./components/RenewingFormDialog.vue";

export default {
  components: {
    RenewingFormDialog
  },

  data() {
    return {
      tblData: [],
      showAdd: false,
      addForm: this.createRenewingModel()
    };
  },

  methods: {
    onConfirm() {
      Promise.resolve().then(() => {
        // reset fields
        this.tblData.push(Object.assign({}, this.addForm));
        console.log(this.addForm);

        this.showAdd = false;
      });
    },
    onCancel() {
      // reset fields
      this.showAdd = false;
    },
    onAdd() {
      Object.assign(this.addForm, this.createRenewingModel());
      this.showAdd = true;
    },
    createRenewingModel() {
      return {
        buildingCode: "",
        roomCode: "",
        phoneNum: "",
        personName: "",
        fromDate: "",
        toDate: "",
        creator: ""
      };
    }
  }
};
</script>

<style>
</style>
