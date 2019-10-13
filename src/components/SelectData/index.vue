<template>
  <el-select :value="value" @change="onChange" filterable allow-create>
    <el-option
      v-for="(item, index) in options"
      :key="index"
      :value="item"
      :label="item.label"
    ></el-option>
  </el-select>
</template>

<script>
export default {
  props: {
    value: {},
    optionsPromise: {
      type: Function,
      required: true
    }
  },

  model: {
    prop: "value",
    event: "change-value"
  },

  data() {
    return {
      options: []
    };
  },

  methods: {
    onChange(selection) {
      this.$emit("change-value", selection);
      this.$emit("change", selection);
    }
  },

  created() {
    this.optionsPromise().then(opts => {
      this.options = opts;
    });
  }
};
</script>

<style>
</style>
