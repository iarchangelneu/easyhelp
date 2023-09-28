<template>
    <div class="page">
        <div class="text-center">
            <h1>EasyHelp.kz</h1>
        </div>

        <div class="form">
            <div class="nado">
                <h1>Регистрация</h1>
                <div class="type">
                    <button :class="{ activeBtn: type == 'seller' }" @click="type = 'seller'">Исполнитель</button>
                    <button :class="{ activeBtn: type == 'buyer' }" @click="type = 'buyer'">Заказчик</button>
                </div>
                <input type="email" v-model="email" placeholder="Эл.почта">
                <input type="password" v-model="password" placeholder="Пароль">
                <input type="password" v-model="password_repeat" placeholder="Повторите пароль">
                <input type="text" v-model="name"
                    :placeholder="type === 'seller' ? 'ФИ или название компании' : 'Ваше имя'">
                <select name="" id="" v-if="type == 'seller'">
                    <option value="" selected disabled>
                        Выберите специализацию
                    </option>
                    <option value="">Текст</option>
                </select>
                <label class="custom-checkbox text-left">
                    <input type="checkbox">
                    <p class="checkbox-text m-0">Я согласен с <NuxtLink to="/terms">пользовательским соглашением
                        </NuxtLink>
                        и <NuxtLink to="/polytics">политикой конфиденциальности</NuxtLink>
                    </p>
                </label>

                <div class="text-center">
                    <button>Зарегистрироваться</button>

                    <span>Уже есть аккаунт? <NuxtLink to="/login">Войти</NuxtLink></span>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            password_repeat: '',
            name: '',
            type: 'seller',
        }
    }
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
        margin-top: -70px;

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