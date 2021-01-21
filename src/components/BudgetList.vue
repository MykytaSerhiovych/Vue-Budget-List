<template>
  <div class="budget-list-wrap">
    <el-card >
      <div slot="header" class="header-wrap">
        <span class="header">{{header}}</span>
        <span class="button-pane">
          <el-button class="button" type="primary" @click="onListShow(1)">income</el-button>
          <el-button class="button" type="primary" @click="onListShow(-1)">outcome</el-button>
          <el-button class="button" type="primary" @click="onListShow()">all</el-button>
        </span>
      </div>
      <template v-if="!isEmpty">
        <div v-for="(item,prop) in list" :key="prop">
          <BudgetListItem :item=item @deleteItem="deleteItem" />
        </div>
      </template>
      <el-alert v-else type="info" :title="emptyTitle" :closable="false" />
    </el-card>
  </div>
</template>

<script>
import BudgetListItem from '@/components/BudgetListItem';
export default {
  name: "BudgetList",
  components: {
    BudgetListItem
  },
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    header: "Budget List",
    emptyTitle: "Empty List!"
  }),
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    }
  },
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id);
    },
    onListShow(param) {
      this.$emit('onListShow', param);
    }
  }
}
</script>

<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: auto;
}
.header-wrap {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.button {
  text-transform: uppercase;
  font-size: 11px;
}
</style>
