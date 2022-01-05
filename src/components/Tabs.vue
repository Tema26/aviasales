<template>
<div>
    <button @click="onClickLowCost">Самый дешёвый</button>
    <button>Самый быстрый</button>
</div>
</template>

<script>
export default {
    methods: {
        onClickLowCost() {
            this.$emit('click-tickets-low-cost')
        }
    }
}
</script>