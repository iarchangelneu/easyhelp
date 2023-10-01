<template>
    <div class="page">

        <h1>
            <span>Вывод средств прошел успешно</span>
            <img src="@/assets/img/successpg.svg" alt="">
        </h1>

    </div>
</template>
<script>
import global from '~/mixins/global';
import axios from 'axios';
export default {
    mixins: [global],
    data() {
        return {
            pathUrl: 'https://easyhelp.kz',
        }
    }
    ,
    methods: {
        sendRequest(reference) {
            const token = this.getAuthorizationCookie();
            const path = `${this.pathUrl}/api/money/success/${reference}`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    console.log(response)
                    if (response.status == 200) {
                        //  window.location.href = '/'
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        },
    },
    mounted() {
        const url = window.location.href;
        const match = url.match(/order_pay_easyhelp_(\d+)/);

        if (match) {
            this.extractedValue = match[0];
            console.log(this.extractedValue);

            this.sendRequest(match[0])
        }
    },
}
</script>
<script setup>
useSeoMeta({
    title: 'Успешная транзакция | EasyHelp',
    ogTitle: 'Успешная транзакция | EasyHelp',
    description: 'Успешная транзакция | EasyHelp',
    ogDescription: 'Успешная транзакция | EasyHelp',
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