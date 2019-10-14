<template>
  <el-select
    :value="value"
    @change="onChange"
    :allow-create="canCreate"
    :filterable="filterable"
    :remote="remote"
  >
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
    },
    filter: {
      type: String
    },
    canCreate: {
      type: Boolean,
      default: true
    }
  },

  model: {
    prop: "value",
    event: "change-value"
  },

  data() {
    return {
      options: [],
      filterable: !!this.filter,
      remote: this.filter === "remote"
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
