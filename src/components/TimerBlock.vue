<template>
    <div class="container-date">
        <h3 class="date-future">{{count}}</h3>
        <span>{{label}}</span>
    </div>
</template>
<script lang="ts" setup>
    defineProps<{ count : string , label: string}>()
</script>
<style scoped>
.date-future{
  font-size: 3rem;
}
</style>