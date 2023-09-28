<template>
    <div class="page">

        <h1>
            <span>Ошибка транзакции</span>
        </h1>

    </div>
</template>
<script>
export default {
    data() {
        return {

        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Неудачная транзакция | EasyHelp',
    ogTitle: 'Неудачная транзакция | EasyHelp',
    description: 'Неудачная транзакция | EasyHelp',
    ogDescription: 'Неудачная транзакция | EasyHelp',
})
</script>
<style lang="scss" scoped>
.page {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;

    h1 {
        display: flex;
        gap: 10px;
        align-items: center;
        margin: 0;

        font-size: 20px;
        font-style: normal;
        font-weight: 400;
        line-height: normal;
        font-family: var(--ral);
    }
}
</style>