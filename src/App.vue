<template>
  <div>
    <select-data
      v-model="sel"
      :optionsPromise="getOpts"
      @change="onChange"
    ></select-data>
    {{ selVal }}
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
      sel: "",
      selVal: ""
    };
  },

  methods: {
    getOpts() {
      return Promise.resolve([{ label: "one", value: "1" }]);
    },
    onChange(selection) {
      if (selection && selection.value) {
        this.selVal = "selected!";
      } else {
        this.selVal = "new!";
      }
    }
  }
};
</script>

<style>
</style>
