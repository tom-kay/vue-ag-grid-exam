<template>
  <div class="grid">
    <ag-grid-vue
      class="ag-theme-alpine"
      style="width: 100%; height: 100vh"
      :columnDefs="columnDefs.columns"
      :rowData="rowData.rows"
      :defaultColDef="defaultColDef"
      rowSelection="multiple"
      animateRows="true"
    >
    </ag-grid-vue>
  </div>
</template>
<script>
import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-alpine.css";
import { AgGridVue } from "ag-grid-vue3";
import { h, onMounted, reactive } from "vue";
import FunCompVue from "./components/FunComp.vue";
import OptionsComp from "./components/OptionsComp.vue";

export default {
  name: "App",
  components: {
    AgGridVue,
    // eslint-disable-next-line vue/no-unused-components
    SimpleComp: {
      setup(props) {
        const { params } = props;
        return () => h("b", "!" + params.value + "!");
      },
    },
    // eslint-disable-next-line vue/no-unused-components
    FunCompVue,
    // eslint-disable-next-line vue/no-unused-components
    OptionsComp,
  },
  setup() {
    const rowData = reactive({ rows: [] });
    const columnDefs = reactive({
      columns: [
        {
          field: "athlete",
          cellRenderer: "FunCompVue",
        },
        {
          field: "age",
          cellRenderer: "OptionsComp",
        },
        { field: "country", cellRenderer: "SimpleComp" },
        {
          field: "year",
          cellRendererSelector: (p) => {
            if (p.value === 2000) {
              return { component: "FunCompVue", params: {} };
            }
            if (p.value === 2008) {
              return { component: "OptionsComp", params: {} };
            }
          },
        },
        { field: "date" },
        { field: "sport" },
        { field: "gold" },
        { field: "silver" },
        { field: "bronze" },
        { field: "total" },
      ],
    });
    const defaultColDef = {
      sortable: true,
      filter: true,
    };

    onMounted(() => {
      fetch("https://www.ag-grid.com/example-assets/olympic-winners.json")
        .then((res) => res.json())
        .then((data) => (rowData.rows = data));
    });

    return { rowData, columnDefs, defaultColDef };
  },
};
</script>
<style scoped></style>
