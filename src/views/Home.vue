<template>
  <div class="home">
    <Table border :options="options" :tableSearch="tableSearch" :columns="columns" :operates="operates(this)" :isAdd="true" :dataApi="dataApi" :refresh="refresh" @addData="$router.push('/configure/spec/editspec')">

  </div>
</template>

<script>
import Table from "@/components/Table";
/* 设置表头 */
const columns = [
  {
    prop: "name",
    label: "工单编号",
    align: "center",
    fixed: true,
  },
  {
    prop: "sortOrder",
    align: "center",
    label: "排序",
  },
];

/* 操作按钮 */
const operates = (that) => [
  {
    label: "编辑",
    size: "mini",
    type: "primary",
    method: (row) => {
      that.editData(row);
    },
  },
  {
    label: "删除",
    type: "warning",
    size: "mini",
    setStyle: {
      marginLeft: "10px",
    },
    method: (row) => {
      that
        .$confirm("确定要删除选中的记录？", "", {
          confirmButtonText: "确定",
          cancelButtonText: "取消",
          type: "warning",
        })
        .then(() => {
          that.delSpec(row);
        })
        .catch(() => {});
    },
  },
];

// 搜索设置
const tableSearch = [
  {
    label: "规格名称",
    value: "name",
    rulesLength: true,
    labelProps: {
      "label-width": "130",
    },
  },
];

export default {
  name: "Home",
  components: {},
  data() {
    return {
      options: {},
      columns,
      operates,
      tableSearch,
      dataApi: "",
      refresh: new Date().getTime(),
    };
  },
};
</script>
