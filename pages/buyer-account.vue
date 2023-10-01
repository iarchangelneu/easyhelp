<template>
    <div class="page">
        <h1>Личный кабинет</h1>

        <div class="navs">
            <div>
                <button :class="{ activeBtn: activeTab == 0 }" @click="activeTab = 0">Мои заказы</button>
                <button :class="{ activeBtn: activeTab == 1 }" @click="activeTab = 1">Транзакции</button>
            </div>
            <div>
                <button :class="{ activeBtn: activeTab == 2 || activeTab == 7 }" @click="activeTab = 2">Обратная
                    связь</button>
                <button :class="{ activeBtn: activeTab == 3 }" @click="activeTab = 3">Аккаунт</button>
            </div>
        </div>

        <div class="sales" v-if="activeTab == 0">
            <div class="sales__item" v-for="item in buys" :key="item.id">
                <img src="@/assets/img/why.png" alt="">

                <div class="item__info">
                    <h1>{{ item.products.name }}</h1>
                    <h1>{{ item.products.price.toLocaleString() + ' ₸' }}</h1>

                    <span class="date">Дата заказа: {{ formatDate(item.date) }}</span>
                    <span>Исполнитель:<br>
                        {{ item.seller.user.first_name }} </span>

                    <button @click="createChat(item.seller.id, item.seller.user.first_name)">Чат с исполнителем</button>
                </div>
            </div>
        </div>

        <div class="chats" v-if="activeTab == 2">
            <div class="chat__item" v-for="chat in chats" :key="chat.id">
                <div>
                    <h2>{{ chat.seller.user.first_name }}</h2>
                    <!-- <small>23.07.2023 14:47</small> -->
                </div>

                <div class="justify-content-end">
                    <button @click="openChat(chat.id, chat.seller.user.first_name)">Открыть чат</button>
                </div>
            </div>
        </div>

        <div class="acc__info" v-if="activeTab == 3">
            <div class="inp">
                <label for="email">Эл.почта</label>
                <input type="email" v-model="email" placeholder="Эл.почта">
                <!-- <div class="text-right">
                    <button class="save">сохранить изменения</button>
                </div> -->
            </div>
            <div class="inp">
                <label for="password">Пароль</label>
                <input type="password" placeholder="Пароль" v-model="password">
                <div class="text-left">
                    <button @click="logOut()">выйти</button>
                </div>
            </div>
        </div>

        <TheTrans v-if="activeTab == 1" :transactions="transactions"></TheTrans>
        <TheMessanger v-if="activeTab == 7" :chatId="chatId" :name="chatName"></TheMessanger>
    </div>
</template>
<script>
import global from '~/mixins/global';
import axios from 'axios';
export default {
    mixins: [global],
    data() {
        return {
            activeTab: 0,
            account: [],
            password: '',
            email: '',
            chats: [],
            seller: [],
            pathUrl: 'https://easyhelp.kz',
            buys: [],
            sendId: null,
            chatId: null,
            myId: null,
            transactions: []

        }
    },
    methods: {
        formatDate(dateString) {
            const date = new Date(dateString);
            const formattedDate = `${date.getDate().toString().padStart(2, '0')}.${(date.getMonth() + 1).toString().padStart(2, '0')}.${date.getFullYear()}`;
            return formattedDate;
        },
        getAccount() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/buyer-lk`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    this.account = response.data
                    this.myId = response.data.id
                    this.transactions = response.data.transactions
                    this.email = response.data.user.email

                })
                .catch(error => console.log(error));
        },
        openChat(chatId, chatName) {
            this.activeTab = 7;
            this.chatId = chatId;
            this.chatName = chatName
        },
        getBuys() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/buyer-lk/my-purchases`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    this.buys = response.data
                })
                .catch(error => {
                    console.error(error)
                })
        },
        createChat(id, name) {
            const token = this.getAuthorizationCookie()
            const csrf = this.getCSRFToken()
            const path = `${this.pathUrl}/api/messanger/new-chat`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .post(path, {
                    buyer: this.myId,
                    seller: id,
                })
                .then(response => {
                    const chatId = response.data.chat_id
                    this.openChat(chatId, name)
                })
                .catch(error => console.log(error))
        },
        getChats() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/messanger/all-chats`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(res => {
                    this.chats = res.data
                })
                .catch(error => console.log(error))
        }
    },
    mounted() {
        const accType = localStorage.getItem('accountType')
        console.log(accType)
        if (accType == 'buyer-account') {
            this.getAccount()
            this.getChats()
            this.getBuys()
        }
        else {
            window.location.href = '/login'
        }
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

    .acc__info {
        display: flex;
        justify-content: center;
        align-items: flex-start;
        gap: 50px;
        margin: 10.417vw 0;

        @media (max-width: 1024px) {
            flex-direction: column;
            justify-content: flex-start;
            align-items: flex-start;
            gap: 20px;
        }

        .save {
            @media (max-width: 1024px) {
                display: none;
            }
        }

        .inp {
            @media (max-width: 1024px) {
                width: 100%;
            }
        }

        label,
        input {
            display: block;
        }

        label {
            margin-bottom: 10px;
            font-size: 16px;
            font-style: normal;
            font-weight: 500;
            line-height: 110%;
            font-family: var(--ral);
            color: #000;
        }

        input {
            border: 2px solid #E3E3E3;
            background: #F6FAFF;
            padding: 10px;

            font-size: 16px;
            font-style: normal;
            font-weight: 400;
            line-height: 130%;
            font-family: var(--ral);
            color: #000;
            width: 23.438vw;

            &::placeholder {
                color: #000;
            }

            @media (max-width: 1024px) {
                width: 100%;
            }
        }

        button {
            border: 2px solid var(--btn);
            background: transparent;
            padding: 10px 20px;
            border-radius: 20px;

            font-size: 16px;
            font-style: normal;
            font-weight: 500;
            line-height: normal;
            text-transform: uppercase;
            font-family: var(--ral);
            color: var(--btn);
            margin-top: 50px;

            transition: all .3s ease;

            &:hover {
                color: #fff;
                background: var(--btn);
            }

            @media (max-width: 1024px) {
                margin-top: 20px;
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
                padding: 10px 20px;
                background: transparent;
                border-radius: 20px;
                border: 2px solid var(--btn);

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