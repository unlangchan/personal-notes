# 常用vuex表格查询模版
```js
// @/store/modules/xxx

const state = {
    list1: {
        // 筛选
        filters: {
          filterKey:'value'
        },
        // 分页
        pagination: {
            pageNum: 1,
            pageSize: 10,
            total: 0,
        },
        // 选择器
        selectOption: {
          filterKey: [
             { label:'key',value: 'value' },
          ]
        },
        // 表头
        theads: [
            { key: 'num', label: '序' },
        ],
        // 数据源
        list: [],
    },
}
const mutations = {
    filterChange(state, input) {
        const { key1, key2, value } = input;
        let dataItem = state[key1];
        dataItem.filters[key2] = value;
        dataItem.pagination.pageNum = 1;
    },
    paginationPageNum(state, input) {
        const { key, value } = input;
         let dataItem = state[key1];
        dataItem.pagination.pageNum = value;
    },
    paginationPageSize(state, input) {
        const { key, value } = input;
        let dataItem = state[key];
        dataItem.pagination.pageSize = value;
        dataItem.pagination.pageNum = 1;
    },
}

const actions = {
    async load({ dispatch }) {
        await dispatch('query');
    },
    async filterChange({ dispatch, state }, input) {
        const { key1, key2, value } = input;
        let dataItem = state[key1];
        dataItem.filters[key2] = value;
        dataItem.pagination.pageNum = 1;
        await dispatch('load');
    },
    async paginationPageNum({ dispatch, state }, input) {
        const { key, value } = input;
         let dataItem = state[key];
        dataItem.pagination.pageNum = value;
        await dispatch('load');
    },
    async paginationPageSize({ dispatch, state }, input) {
        const { key, value } = input;
        let dataItem = state[key];
        dataItem.pagination.pageSize = value;
        dataItem.pagination.pageNum = 1;
        await dispatch('load');
    },
}

const getters = {
  view:(state)=>{
    const { list1 } = state;
    return {
      ...list1,
    }
  }
}

export default {
  namespaced: true,
  state,
  mutations,
  actions,
  getters
}
```

```html
<!-- @/xxx.vue template -->
<!-- <template> -->
  <div class="container">
    <div class="filterbox">
      <el-input
        size="mini"
        class="filter-item filter-input"
        :value="view.filters.filterKey"
        @change="handleChange($event, 'list1', 'filterKey')"
      ></el-input>
      <el-select
        size="mini"
        class="filter-item filter-select"
        clearable
        :value="view.filters.filterKey"
        @change="handleChange($event, 'list1', 'filterKey')"
      >
        <el-option
          v-for="(item, index) of view.selectOption.filterKey"
          :key="index"
          :label="item.label"
          :value="item.value"
        >
        </el-option>
      </el-select>
    </div>
    <el-table :data="view.list">
      <el-table-column
        v-for="(item, index) of view.theads"
        :key="index"
        :prop="item.key"
        :label="item.label"
        :width="item.width"
      ></el-table-column>
    </el-table>
    <el-pagination
      background
      layout="sizes, prev, pager, next,total"
      :page-sizes="[10, 20, 30, 50]"
      :page-size="view.pagination.pageSize"
      :current-page="view.pagination.pageNum"
      :total="view.pagination.total"
      @current-change="handlePageNum($event, 'list1')"
      @size-change="handlePageSize($event, 'list1')"
    >
    </el-pagination>
  </div>
<!-- </template> -->
```

```scss
// @/xxx.vue style
// <style style lang="scss" scoped>
.container {
  .filterbox {
  }
  .filter-item {
  }
  .filter-input {
  }
  .el-table {
  }
  .el-pagination {
  }
}
// </style>
```

```js
// @/xxx.vue script
// <script>
import { mapGetters } from "vuex";
const namespaced = "xxx";
export default {
  name: namespaced,
  computed: {
    ...mapGetters({
      view: `${namespaced}/view`,
    }),
  },
  methods: {
    async handlePageNum(value, key) {
      const { dispatch } = this.$store;
      await dispatch(`${namespaced}/paginationPageNum`, { value, key });
    },
    async handlePageSize(value, key) {
      const { dispatch } = this.$store;
      await dispatch(`${namespaced}/paginationPageSize`, { value, key });
    },
    async handleChange(value, key1, key2) {
      const { dispatch } = this.$store;
      await dispatch(`${namespaced}/filterChange`, { value, key1, key2 });
    },
  },
};
// </script>

```