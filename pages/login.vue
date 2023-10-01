<template>
    <div class="page">
        <div class="text-center">
            <h1>EasyHelp.kz</h1>
        </div>

        <div class="form">
            <div class="nado">
                <h1>Авторизация</h1>
                <input type="email" v-model="email" placeholder="Эл.почта">
                <input type="password" v-model="password" placeholder="Пароль">
                <div class="text-center">
                    <button @click="login()">Войти</button>

                    <span>Еще нет аккаунта? <NuxtLink to="/register">Зарегистрироваться</NuxtLink></span>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import global from '~/mixins/global';
import axios from 'axios';
export default {
    mixins: [global],
    data() {
        return {
            email: '',
            password: '',
            password_repeat: '',
            name: '',
            type: 'seller',
            pathUrl: 'https://easyhelp.kz',
        }
    },
    methods: {
        login() {
            const path = `${this.pathUrl}/api/main/authorization`
            const csrf = this.getCSRFToken()

            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .post(path, { username: this.email, password: this.password })
                .then((res) => {



                    document.cookie = `Authorization=${res.data.token}; expires=Fri, 31 Dec 2023 23:59:59 GMT; path=/`;
                    localStorage.setItem('accountType', res.data.redirect_url)
                    if (res.data.redirect_url == 'buyer-account') {
                        window.location.href = '/'
                    }
                    if (res.data.redirect_url == 'seller-account') {
                        window.location.href = '/seller-account'
                    }


                    console.log(res)
                })
                .catch((error) => {
                    console.log(error);
                    this.error = error.response.data.non_field_errors.toString()
                });
        },
        getCategoryName(categoryId) {
            const category = this.categories.find((c) => c.id === categoryId);
            return category ? category.name : "";
        },
    },
    mounted() {
        const accType = localStorage.getItem('accountType')
        if (accType == 'buyer-account') {
            window.location.href = '/buyer-account'
        }
        else if (accType == 'seller-account') {
            window.location.href = '/seller-account'
        }
        else {
            console.log('not authorized')
        }

    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Авторизация | EasyHelp',
    ogTitle: 'Авторизация | EasyHelp',
    description: 'Авторизация | EasyHelp',
    ogDescription: 'Авторизация | EasyHelp',
})
</script>
<style lang="scss" scoped>
.page {
    padding: 80px 20px 0;

    .form {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin-top: -190px;

        @media (max-width: 1024px) {
            width: 100%;
            height: auto;
            margin-top: 70px;
        }

        .nado {
            @media (max-width: 1024px) {
                width: 100%;
            }
        }

        .text-center {
            button {
                border-radius: 10px;
                border: 2px solid #000;
                background: #000;
                padding: 10px 30px;

                font-size: 20px;
                font-style: normal;
                font-weight: 600;
                line-height: 130%;
                font-family: var(--ral);
                color: #fff;

                @media (max-width: 1024px) {
                    font-size: 16px;
                }
            }

            span {
                display: block;
                margin: 20px 0 0;

                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 110%;
                font-family: var(--ral);
                color: #000;

                a {
                    color: #000;
                    text-decoration: underline;
                }
            }
        }

        .type {
            display: flex;
            gap: 47px;
            margin: 0 0 30px;

            @media (max-width: 1024px) {
                gap: 20px;
                margin: 0 0 20px;
            }

            .activeBtn {
                background: #000;
                color: #fff;
                border: 1px solid #000;
            }

            button {
                flex: 1;
                border-radius: 10px;
                border: 1px solid #E3E3E3;
                background: #F6FAFF;
                padding: 10px 0;

                font-size: 20px;
                font-style: normal;
                font-weight: 600;
                line-height: 130%;
                font-family: var(--ral);
                color: #000;

                transition: all .3s ease;

                @media (max-width: 1024px) {
                    font-size: 16px;
                }
            }
        }

        p {
            max-width: 407px;
            font-size: 16px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--ral);
            color: #000;

            @media (max-width: 1024px) {
                max-width: 100%;
                font-size: 12px;
            }

            a {
                text-decoration: underline;
                color: #000;
            }
        }

        input,
        select {
            display: block;
            width: 446.995px;
            background: #F6FAFF;
            border: 1px solid #E3E3E3;
            border-radius: 10px;
            padding: 10px 15px;

            font-size: 16px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--ral);
            color: #000;
            margin-bottom: 30px;

            &::placeholder {
                color: #000;
            }

            @media (max-width: 1024px) {
                width: 100%;
            }
        }

        select {
            margin-bottom: 20px !important;
        }

        h1 {
            font-size: 64px;
            font-style: normal;
            font-weight: 600;
            line-height: 130%;
            font-family: var(--ral);
            color: #000;
            margin: 0 0 30px;
            text-align: center;


            @media (max-width: 1024px) {
                font-size: 32px;
                margin: 0 0 20px;
            }
        }
    }

    h1 {
        font-size: 64px;
        font-style: normal;
        font-weight: 600;
        line-height: normal;
        font-family: var(--ral);
        color: var(--btn);
        margin: 0;

        @media (max-width: 1024px) {
            font-size: 48px;
        }
    }
}

// .custom-checkbox p {
//     font-family: var(--ral);
//     font-size: 16px;
//     font-style: normal;
//     font-weight: 400;
//     line-height: 130%;
//     color: #000;
//     white-space: nowrap;
//     text-transform: uppercase;
// }

.custom-checkbox input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    border-radius: 3px;
}

.custom-checkbox .checkbox-text:before {
    content: '';
    display: inline-block;
    vertical-align: middle;
    width: 20px;
    height: 20px;
    margin-right: 10px;
    border: 2px solid #000;
    border-radius: 3px;
    margin-bottom: 3px;
}

.custom-checkbox input[type="checkbox"]:checked+.checkbox-text:before {
    content: url('@/assets/img/check.svg');
    font-size: 16px;
    color: black;
    text-align: center;
    line-height: 20px;
    background: transparent;
}

.custom-checkbox {
    margin-bottom: 22px;

}

.custom-checkbox:last-child {
    margin-bottom: 0 !important;

    @media (max-width: 1024px) {
        margin-bottom: 22px !important;
    }
}
</style>