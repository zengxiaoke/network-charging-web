<template>
  <div>
    <el-dialog title="新开通" visible width="700px">
      <el-form :model="addForm" label-width="200px">
        <el-form-item label="房号">
          <select-data
            v-model="addForm.roomCode"
            filter="local"
            :optionsPromise="getOpts"
            @change="onChange"
          ></select-data>
        </el-form-item>
        <el-form-item label="楼号">
          <el-input
            v-model="addForm.buildingCode"
            :disabled="!newRoom"
            class="text-box"
          ></el-input>
        </el-form-item>
        <el-form-item label="住户姓名">
          <select-data
            v-model="addForm.personName"
            filter="local"
            :optionsPromise="getOpts"
            @change="onChangePerson"
          ></select-data>
        </el-form-item>
        <el-form-item label="联系电话">
          <el-input
            v-model="addForm.phoneNum"
            :disabled="!newPerson"
            class="text-box"
          ></el-input>
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
          <select-data
            v-model="addForm.creator"
            :canCreate="false"
            :optionsPromise="getEmployees"
          ></select-data>
        </el-form-item>
      </el-form>

      <template slot="footer">
        <el-button type="primary" @click="onConfirm">确认</el-button>
        <el-button @click="onCancel">取消</el-button>
      </template>
    </el-dialog>
  </div>
</template>

<script>
import SelectData from "./components/SelectData/index.vue";

export default {
  components: {
    SelectData
  },

  data() {
    return {
      tblData: [],
      showAdd: false,
      addForm: this.createRenewingModel(),
      newRoom: false,
      newPerson: false
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
    },
    getOpts() {
      return Promise.resolve([
        { label: "one", value: "1" },
        { label: "two", value: "2" }
      ]);
    },
    onChange(selection) {
      this.newRoom = !(selection && selection.value);
      this.addForm.buildingCode = this.newRoom ? "" : selection.value;
    },
    onChangePerson(selection) {
      this.newPerson = !(selection && selection.value);
      this.addForm.phoneNum = this.newPerson ? "" : selection.value;
    },
    getEmployees() {
      return Promise.resolve([
        { label: "5600033", value: "5600033" },
        { label: "5600014", value: "5600014" }
      ]);
    }
  }
};
</script>

<style lang="less">
.text-box {
  width: 182px;
}
</style>
