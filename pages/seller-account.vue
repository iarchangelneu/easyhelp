<template>
    <div class="page">

        <h1>Личный кабинет</h1>

        <div class="navs">
            <div>
                <button @click="activeTab = 0"
                    :class="{ activeBtn: activeTab == 0 || activeTab == 5 || activeTab == 6 }">Мои
                    услуги</button>
                <button @click="activeTab = 1" :class="{ activeBtn: activeTab == 1 }">Выполненные</button>
            </div>
            <div>
                <button @click="activeTab = 2" :class="{ activeBtn: activeTab == 2 }">Транзакции</button>
                <button @click="activeTab = 3" :class="{ activeBtn: activeTab == 3 || activeTab == 7 }">Обратная
                    связь</button>
            </div>
            <div>
                <button @click="activeTab = 4" :class="{ activeBtn: activeTab == 4 }">Аккаунт</button>
            </div>
        </div>
        <div class="addproduct" v-if="activeTab == 0">
            <button @click="activeTab = 5">
                <span>Добавить товар</span>
                <img src="@/assets/img/filter.svg" alt="">
            </button>
        </div>
        <div class="sales" v-if="activeTab == 0">
            <div class="sales__item">
                <img src="@/assets/img/why.png" alt="">

                <div class="item__info">
                    <h1>Услуга Генеральная уборка</h1>
                    <h1>80 000 ₸</h1>


                    <button @click="activeTab = 6">Изменить</button>
                    <NuxtLink to="/product/1">Страница услуги</NuxtLink>
                </div>
            </div>
            <div class="sales__item">
                <img src="@/assets/img/why.png" alt="">

                <div class="item__info">
                    <h1>Услуга Генеральная уборка</h1>
                    <h1>80 000 ₸</h1>


                    <button>Изменить</button>
                    <NuxtLink to="/product/1">Страница услуги</NuxtLink>
                </div>
            </div>
            <div class="sales__item">
                <img src="@/assets/img/why.png" alt="">

                <div class="item__info">
                    <h1>Услуга Генеральная уборка</h1>
                    <h1>80 000 ₸</h1>


                    <button>Изменить</button>
                    <NuxtLink to="/product/1">Страница услуги</NuxtLink>
                </div>
            </div>

        </div>
        <div class="sales" v-if="activeTab == 1">
            <div class="sales__item">
                <img src="@/assets/img/why.png" alt="">

                <div class="item__info">
                    <h1>Услуга Генеральная уборка</h1>
                    <h1>80 000 ₸</h1>
                    <span>Дата исполнения: 12.08.2023</span>

                    <NuxtLink to="/product/1" style="margin-top: auto; margin-bottom: 15px;">Услуга</NuxtLink>
                    <button @click="activeTab = 7">Чат с заказчиком</button>

                </div>
            </div>

        </div>
        <div class="chats" v-if="activeTab == 3">
            <div class="chat__item">
                <div>
                    <h2>alex.ivanov@gmail.com</h2>
                    <!-- <small>23.07.2023 14:47</small> -->
                </div>

                <div class="justify-content-end">
                    <button @click="activeTab = 7">Открыть чат</button>
                </div>
            </div>
            <div class="chat__item">
                <div>
                    <h2>alex.ivanov@gmail.com</h2>
                    <!-- <small>23.07.2023 14:47</small> -->
                </div>

                <div class="justify-content-end">
                    <button @click="activeTab = 7">Открыть чат</button>
                </div>
            </div>
            <div class="chat__item">
                <div>
                    <h2>alex.ivanov@gmail.com</h2>
                    <!-- <small>23.07.2023 14:47</small> -->
                </div>

                <div class="justify-content-end">
                    <button @click="activeTab = 7">Открыть чат</button>
                </div>
            </div>
        </div>


        <div class="accs" v-if="activeTab == 4">
            <div class="account__profile">
                <div class="profile__left">
                    <div class="avatar w-100">
                        <div class="avik">
                            <label for="fileInput" class="editava ml-0" @click="openFileInput">
                                <span>Изменить фото</span>
                            </label>
                            <input type="file" id="fileInput" ref="fileInput" accept="image/*"
                                style="display: none !important;" @change="handleFileChange">
                            <!-- Используем avatarUrl для отображения выбранного изображения или дефолтного изображения -->
                            <img :src="avatarUrl" alt="" loading="lazy">
                        </div>

                    </div>
                    <div class="data">
                        <label for="name">Отображаемое Имя</label>
                        <input type="text" placeholder="Ваше имя" class="w-100" v-model="name">
                    </div>
                    <div class="data">
                        <label for="name">E-mail</label>
                        <input class="w-100" type="email" placeholder="E-mail" v-model="email">
                    </div>

                    <div class="data">
                        <label for="name">Пароль</label>
                        <input class="w-100" type="password" placeholder="Пароль">
                    </div>

                </div>
                <div class="profile__right w-100">
                    <label for="desc">Описание профиля</label>
                    <textarea name="desc" id="desc" cols="30" rows="17" v-model="description"></textarea>
                    <div class="mt-4">
                        <label for="tabs mt-4">Особенности (До 4)</label>
                        <div class="custom-textarea">
                            <textarea class="features-list" сols="30" rows="4" ref="featuresList2"
                                v-model="courseFeaturesText" @keydown="handleKeyDown"></textarea>
                        </div>
                    </div>


                    <div class="buttons">
                        <button @click="editAccount()" ref="edit">Сохранить изменения</button>
                        <button @click="logOut()">Выйти из аккаунта</button>
                    </div>
                </div>
            </div>
        </div>

        <TheTrans v-if="activeTab == 2" :transactions="transactions"></TheTrans>
        <CreateProduct v-if="activeTab == 5"></CreateProduct>
        <EditProduct v-if="activeTab == 6" :productId="sendId"></EditProduct>
        <TheMessanger v-if="activeTab == 7" :chatId="chatId" :name="chatName"></TheMessanger>
    </div>
</template>
<script>
export default {
    data() {
        return {
            email: '',
            activeTab: 0,
            transactions: [],
            chatId: null,
            chatName: '',
            sendId: null,
            courseFeaturesText: '',
        }
    },
    methods: {
        handleKeyDown(event) {
            if (event.key === 'Backspace' && !this.courseFeaturesText) {
                event.preventDefault();
                return;

            }

            const lines = this.courseFeaturesText.split('\n');
            if (lines.length >= 4 && event.key === 'Enter') {
                event.preventDefault();
                this.$refs.featuresList2.style.borderColor = 'red'
                return;
            }
        },
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Личный кабинет | EasyHelp',
    ogTitle: 'Личный кабинет | EasyHelp',
    description: 'Личный кабинет | EasyHelp',
    ogDescription: 'Личный кабинет | EasyHelp',
})
</script>
<style lang="scss" scoped>
.page {
    padding: 150px 100px 80px;

    @media (max-width: 1600px) {
        padding: 150px 50px 80px;
    }

    @media (max-width: 1024px) {
        padding: 150px 20px 50px;
    }

    .accs {
        .buttons {
            display: flex;
            justify-content: flex-start;
            align-items: center;
            gap: 20px;
            margin-top: 30px;

            @media (max-width: 1024px) {
                flex-direction: column;
                align-items: flex-start;

            }

            button,
            a {
                padding: 10px 20px;
                border: 2px solid var(--btn);
                border-radius: 20px;
                background: transparent;

                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--ral);
                text-transform: uppercase;
                color: var(--btn);
                transition: all .3s ease;

                &:hover {
                    color: #fff;
                    background: var(--btn);
                }


                @media (max-width: 1024px) {
                    flex: 1;
                }
            }
        }
    }

    .account__profile {
        margin-top: 38px;
        display: flex;
        gap: 54px;

        @media (max-width: 1024px) {
            flex-direction: column;
            margin-top: 20px;
        }

        label,
        input {
            display: block;
        }

        label {
            font-size: 16px;
            font-style: normal;
            font-weight: 500;
            line-height: 110%;
            font-family: var(--ral);
            color: #000;
            margin-left: 10px;
        }

        input {
            border: 1px solid #E3E3E3;
            border-radius: 0;
            padding: 10px;
            width: 336px;

            font-size: 16px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--ral);
            color: #000;
            background: #F6FAFF;

            @media (max-width: 1024px) {
                width: 100%;
                max-width: 100%;
                display: inline;
            }
        }


        .profile__left {
            //  width: 100%;

            .data {
                margin-top: 20px;
            }

            .avatar {
                display: flex;
                gap: 20px;
                align-items: flex-start;

                @media (max-width: 1024px) {
                    flex-direction: column;
                    align-items: center;
                    width: 100%;
                }

                .avik {
                    border-radius: 0;
                }

                img {
                    width: 16.667vw;
                    height: 14.323vw;
                    object-fit: cover;

                    @media (max-width: 1024px) {
                        width: 100%;
                        height: 300px;
                    }
                }

                div {
                    position: relative;
                    overflow: hidden;

                    &:last-child {
                        @media (max-width: 1024px) {
                            width: 100%;
                        }
                    }



                    .editava {
                        position: absolute;
                        display: flex !important;
                        justify-content: center;
                        align-items: center;
                        transition: all .3s ease;
                        transform: scaleY(0);
                        width: 100%;
                        height: 100%;
                        border-radius: 0;
                        background: rgba(246, 246, 246, 0.30);
                        cursor: pointer;

                        top: 0;

                        span {
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            padding: 10px;
                            background: #fff;
                            border-radius: 0;

                            font-size: 10.755px;
                            font-style: normal;
                            font-weight: 500;
                            line-height: 130%;
                            text-decoration-line: underline;
                            font-family: var(--ral);
                            color: #000;
                            cursor: pointer;
                        }

                    }

                    &:hover .editava {
                        transform: scaleY(1)
                    }
                }
            }
        }

        .profile__right {
            textarea {
                width: 100%;
                // max-width: ;
                display: block;
                background: #F6FAFF;
                border-radius: 0;
                border: 1px solid #E3E3E3;
                padding: 20px;

                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--ral);
                color: #000;
            }
        }
    }

    .chats {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(546px, 1fr));
        gap: 41px;
        grid-auto-flow: dense;
        margin-top: 40px;

        @media (max-width: 1024px) {
            grid-template-columns: repeat(auto-fill, minmax(100%, 1fr));
            gap: 20px;
        }

        .chat__item {
            background: #F6FAFF;
            padding: 30px 20px;
            border: 1px solid #E3E3E3;

            .justify-content-end {
                @media (max-width: 1024px) {
                    justify-content: flex-start !important;
                }

            }

            div {
                display: flex;
                justify-content: space-between;
                align-items: center;

                h2,
                small {
                    margin: 0;
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: normal;
                    font-family: var(--ral);
                    color: #000;
                }

                button {
                    margin-top: 30px;
                    padding: 10px 30px;
                    background: transparent;
                    border: 2px solid var(--btn);
                    border-radius: 20px;

                    font-size: 16px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--ral);
                    color: var(--btn);

                    transition: all .3s ease;

                    &:hover {
                        color: #fff;
                        background: var(--btn);
                    }
                }
            }
        }
    }

    .addproduct {
        display: flex;
        justify-content: center;
        margin-top: 30px;

        button {
            display: flex;
            align-items: center;
            gap: 7px;
            padding: 10px 20px;
            background: #8BBAFF;
            border-radius: 20px;
            border: 0;

            font-size: 16px;
            font-style: normal;
            font-weight: 600;
            line-height: 130%;
            font-family: var(--ral);
            color: #fff;
        }
    }

    .sales {
        margin-top: 30px;
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(550px, 1fr));
        gap: 30px;
        grid-auto-flow: dense;

        @media (max-width: 490px) {
            grid-template-columns: repeat(auto-fill, minmax(100%, 1fr));
        }

        .sales__item {
            border: 1px solid #E3E3E3;
            background: #F6FAFF;
            padding: 20px;
            display: flex;
            gap: 20px;

            img {
                width: 200px;
                height: 210px;
                object-fit: cover;

                @media (max-width: 1024px) {
                    width: 100px;
                    height: 100px;
                }
            }

            @media (max-width: 1024px) {
                gap: 10px;
            }

            .item__info {
                display: flex;
                flex-direction: column;

                h1 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 600;
                    line-height: 130%;
                    font-family: var(--btn);
                    color: #000;
                    margin-bottom: 10px;

                    @media (max-width: 1024px) {
                        font-size: 16px;
                    }

                }

                .date {
                    margin-top: 10px;
                }

                span {
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 600;
                    line-height: 130%;
                    font-family: var(--ral);
                    color: #000;
                    display: block;
                    margin: 0 0 10px;

                    @media (max-width: 1024px) {
                        font-size: 12px;
                    }

                }
            }

            button {
                margin-top: auto;
                margin-bottom: 15px;
            }

            button,
            a {
                padding: 10px 20px;
                background: transparent;
                border-radius: 20px;
                border: 2px solid var(--btn);
                text-align: center;

                font-family: var(--ral);
                color: var(--btn);
                font-size: 16px;
                font-style: normal;
                font-weight: 600;
                line-height: 130%;

                transition: all .3s ease;

                @media (max-width: 1024px) {
                    font-size: 12px;
                }

                &:hover {
                    background: var(--btn);
                    color: #fff;
                }
            }
        }
    }

    .navs {
        display: flex;
        justify-content: center;
        gap: 30px;

        @media (max-width: 1024px) {
            gap: 20px;
            flex-direction: column;
        }

        div {
            display: flex;
            gap: 30px;

            @media (max-width: 1024px) {
                gap: 20px;
            }

            .activeBtn {
                background: #8BBAFF !important;
                color: #fff !important;
                border: 2px solid #8BBAFF !important;
            }

            button {
                padding: 10px 20px;
                background: transparent;
                border: 2px solid var(--btn);
                border-radius: 20px;

                color: var(--btn);
                font-family: var(--ral);
                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;

                transition: all .3s ease;

                @media (max-width: 1024px) {
                    flex: 1;
                }
            }
        }
    }

    h1 {
        font-size: 40px;
        font-style: normal;
        font-weight: 600;
        line-height: 130%;
        font-family: var(--ral);
        color: #000;
        margin: 0 0 30px;

        @media (max-width: 1024px) {
            font-size: 20px;
            margin: 0 0 20px;
        }
    }
}
</style>