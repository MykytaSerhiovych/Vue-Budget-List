<template>
    <div class="total-value">
        <template v-if="total > 0">
            <div class="positive-balance">
                Balance: {{total}}
            </div>
        </template>
        <template v-if="total < 0">
            <div class="negative-balance">
                Balance: {{total}}
            </div>
        </template>
        <template v-if="total == 0">
            <div class="zero-balance">
                Balance: {{total}}
            </div>
        </template>
    </div>
</template>

<script>
export default {
    name: 'TotalBalance',
    props: {
        total: {
            type: Number,
            default: 0
        }
    }
}
</script>

<style scoped>
.total-value {
    font-size: 26px;
    padding: 20px;
    text-transform: uppercase;
    text-align: center;
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
