<template>
  <div class="page">
    <div class="page-btns">
      <el-button type="primary" size="mini" @click="handleExport"
        >导出
      </el-button>

      <!-- input file 导入 -->
      <label for="file" style="margin: 0 8px; line-height: 28px">导入</label>
      <input
        id="file"
        type="file"
        style="display: none"
        @change="handleImport1"
      />

      <!-- element-ui upload -->
      <el-upload
        action=""
        :auto-upload="false"
        :show-file-list="false"
        :before-upload="() => false"
        :on-change="handleImport2"
      >
        <el-button type="primary" size="mini">上传 </el-button>
      </el-upload>
    </div>
    <sheet ref="sheet" v-model="sheetData" />
  </div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: "Dashboard",
  data() {
    return {
      sheetData: [
        {
          name: "sheet1",
          rows: {
            0: {
              cells: {
                0: {
                  text: "name",
                },
                1: {
                  text: "小明",
                },
              },
            },
            1: {
              cells: {
                0: {
                  text: "age",
                },
                1: {
                  text: "20",
                },
              },
            },
            len: 100,
          },
        },
      ],
    };
  },
  computed: {
    ...mapGetters(["name"]),
  },
  methods: {
    handleExport() {
      this.$refs.sheet.export("报表2022-07-16");
    },
    handleImport1(files) {
      this.$refs.sheet.import(files);
    },
    handleImport2(file) {
      this.$refs.sheet.import(file.raw);
    },
  },
};
</script>

<style lang="scss" scoped>
.page {
  height: calc(100vh - 118px);
  padding: 0 16px;
  .page-btns {
    display: flex;
    margin: 20px 0;
  }
}
</style>
