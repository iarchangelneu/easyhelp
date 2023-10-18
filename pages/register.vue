<template>
    <div class="page">
        <div class="text-center">
            <h1>EasyHelp.kz</h1>
        </div>

        <div class="form">
            <div class="nado">
                <h1>Регистрация</h1>
                <div class="type">
                    <button :class="{ activeBtn: userType == 'seller' }" @click="userType = 'seller'">Исполнитель</button>
                    <button :class="{ activeBtn: userType == 'buyer' }" @click="userType = 'buyer'">Заказчик</button>
                </div>
                <input type="email" v-model="email" placeholder="Эл.почта" ref="email">
                <input type="password" v-model="password" placeholder="Пароль" ref="password">
                <input type="password" v-model="repeat__password" placeholder="Повторите пароль" ref="repeat__password">
                <input type="text" v-model="name"
                    :placeholder="userType === 'seller' ? 'ФИ или название компании' : 'Ваше имя'" ref="name">
                <select name="" id="" v-if="userType == 'seller'" v-model="selectedCategory" ref="select">
                    <option value="" selected disabled>
                        Выберите специализацию
                    </option>
                    <option v-for="(category, index) in categories" :key="index" :value="category.id">{{ category.name
                    }}
                    </option>
                </select>
                <label class="custom-checkbox text-left">
                    <input type="checkbox" v-model="checked">
                    <p class="checkbox-text m-0" ref="checked">Я согласен с <NuxtLink to="/terms">пользовательским
                            соглашением
                        </NuxtLink>
                        и <NuxtLink to="/polytics">политикой конфиденциальности</NuxtLink>
                    </p>
                </label>

                <div class="text-center">
                    <button @click="register()">Зарегистрироваться</button>

                    <span>Уже есть аккаунт? <NuxtLink to="/login">Войти</NuxtLink></span>
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
            repeat__password: '',
            name: '',
            userType: 'seller',
            selectedCategory: 0,
            checked: false,
            error: '',
            pathUrl: 'https://easyhelp.kz',
            categories: [
                { id: 1, name: 'Клининг' },
                { id: 2, name: 'Ремонт дома' },
                { id: 3, name: 'Сантехника' },
                { id: 4, name: 'Строительство' },
                { id: 5, name: 'Электрика' },
                { id: 6, name: 'Сборка мебели' },
                { id: 7, name: 'Установка' },
                { id: 8, name: 'Погрузка' },
            ],
        }
    },
    methods: {
        register() {
            const buyer = `${this.pathUrl}/api/main/registration/buyer`
            const seller = `${this.pathUrl}/api/main/registration/seller`
            const csrf = this.getCSRFToken()

            if (this.email !== '') {
                this.error = ''
                this.$refs.email.style.borderColor = '#E3E3E3'

                if (this.password != 0 && this.password == this.repeat__password) {
                    this.$refs.password.style.borderColor = '#E3E3E3'
                    this.$refs.repeat__password.style.borderColor = '#E3E3E3'
                    this.error = ''

                    if (this.checked) {
                        this.$refs.checked.style.color = '#E3E3E3'
                        if (this.name !== '') {
                            this.$refs.name.style.borderColor = '#E3E3E3'
                            this.error = ''
                            if (this.userType == 'seller') {
                                if (this.selectedCategory > 0) {


                                    this.$refs.select.style.borderColor = '#E3E3E3'
                                    this.error = ''
                                    axios.defaults.headers.common['X-CSRFToken'] = csrf;
                                    axios
                                        .post(seller, { first_name: this.name, password: this.password, username: this.email, email: this.email, category: this.selectedCategory })
                                        .then((res) => {

                                            document.cookie = `Authorization=${res.data.token}; expires=Fri, 31 Dec 2023 23:59:59 GMT; path=/`;
                                            console.log(res)
                                            localStorage.setItem('accountType', res.data.redirect_url)
                                            window.location.href = res.data.redirect_url
                                        })
                                        .catch((error) => {
                                            if (error.response.data.detail) {
                                                this.error = error.response.data.detail
                                            }
                                            this.error = 'Ошибка на стороне сервера'
                                            console.log(error.response);
                                        });
                                }
                                else {
                                    this.error = 'Выберите специализацию'
                                    this.$refs.select.style.borderColor = 'red'
                                }

                            }
                            else {
                                axios.defaults.headers.common['X-CSRFToken'] = csrf;
                                this.error = ''
                                axios
                                    .post(buyer, { first_name: this.name, email: this.email, password: this.password, username: this.email, email: this.email })
                                    .then((res) => {

                                        document.cookie = `Authorization=${res.data.token}; expires=Fri, 31 Dec 2023 23:59:59 GMT; path=/`;
                                        console.log(res)
                                        localStorage.setItem('accountType', res.data.redirect_url)
                                        window.location.href = '/'
                                    })
                                    .catch((error) => {
                                        console.log(error.responseS);
                                        this.error = error.response.data.detail
                                    });
                            }

                        }
                        else {
                            this.error = 'Вы не заполнили имя'
                            this.$refs.name.style.borderColor = 'red'
                        }
                    }
                    else {
                        this.$refs.checked.style.color = 'red'
                        this.error = 'Вы не согласились с условиями'
                    }
                }
                else {
                    this.error = 'Пароли не совпадают'
                    this.$refs.password.style.borderColor = 'red'
                    this.$refs.repeat__password.style.borderColor = 'red'
                }
            }
            else {
                this.error = 'Вы не указали почту'
                this.$refs.email.style.borderColor = 'red'
            }
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
    },
}
</script>
<script setup>
useSeoMeta({
    title: 'Регистрация | EasyHelp',
    ogTitle: 'Регистрация | EasyHelp',
    description: 'Регистрация | EasyHelp',
    ogDescription: 'Регистрация | EasyHelp',
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