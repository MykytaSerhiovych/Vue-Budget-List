<template>
    <div class="list-item">
         <template v-if="item.value < 0">
            <i class="el-icon-bottom"></i>
            <span class="budget-comment negative-balance">{{ item.comment }}</span>
            <span class="budget-value negative-balance">{{ item.value }}</span>
        </template>
        <template v-if="item.value > 0">
            <i class="el-icon-top"></i>
            <span class="budget-comment positive-balance">{{ item.comment }}</span>
            <span class="budget-value positive-balance">{{ item.value }}</span>
        </template>
        <el-button type="danger" size="mini" @click="deleteItem(item.id)">Delete</el-button>
    </div>
</template>

<script>
export default {
    name: 'BudgetListItem',
    data: () =>({}),
    props: {
        item: {
            type: Object,
            default: () => ({})
        }
    },
    methods: {
        deleteItem(id) {
            this.$emit('deleteItem', id);
        }
    }
}
</script>

<style scoped>
.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;

}
.list-item i {
    margin-right: 5px;
}
.budget-value {
  font-weight: 700;
  margin-left: auto;
  margin-right: 20px;
}
.positive-balance{
  color: green;
}
.negative-balance{
  color: #ad1010;
}
.zero-balance{
  color: #000;
}
</style>
