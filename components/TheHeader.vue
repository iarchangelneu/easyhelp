<template>
    <header v-if="!hideHeaderOnPages.includes($route.name)">
        <div class="header__body">
            <div class="leftside">
                <NuxtLink to="/catalog">Каталог услуг</NuxtLink>
                <NuxtLink to="/experts">Исполнители</NuxtLink>
            </div>

            <NuxtLink to="/" class="logopc"><img src="@/assets/img/headerlogo.svg" class="mr-5 pr-5" alt=""></NuxtLink>
            <NuxtLink to="/" class="logomob "><img src="@/assets/img/headerlogomob.svg" alt=""></NuxtLink>

            <div v-if="accountUrl !== '/seller-account' && accountUrl !== '/buyer-account'">
                <NuxtLink to="/login">Вход / Регистрация</NuxtLink>
            </div>
            <div v-else>
                <span class="balance" v-if="userBalance !== null">{{ userBalance == null ? '0 ₸' :
                    userBalance.toLocaleString()
                    + ' ₸' }}</span>
                <NuxtLink to="/withdrawal" class="cash">
                    <img src="@/assets/img/cash.svg" alt="">
                </NuxtLink>
                <NuxtLink to="/cart" v-if="accountUrl == '/buyer-account'">
                    <img src="@/assets/img/cart.svg" alt="">
                </NuxtLink>
                <NuxtLink :to="accountUrl">
                    <img src="@/assets/img/acc.svg" alt="">
                </NuxtLink>

                <div class="burg">
                    <input id="menu__toggle" class="d-none" type="checkbox" />
                    <label class="menu__btn" for="menu__toggle" @click="menuOpen = !menuOpen">
                        <span></span>
                    </label>
                </div>
            </div>
        </div>

        <div class="mobmenu" :class="{ active: menuOpen }">
            <div class="links">
                <NuxtLink to="/catalog">Каталог услуг</NuxtLink>
                <NuxtLink to="/experts">Исполнители</NuxtLink>
            </div>
            <div class="links">
                <NuxtLink :to="accountUrl">Профиль</NuxtLink>
                <NuxtLink to="/refill" class="withdrawal">
                    <span v-if="userBalance !== null">{{ userBalance == null ? '0 ₸' : userBalance.toLocaleString()
                        + ' ₸' }}</span>
                    <img src="@/assets/img/cash2.svg" alt="">
                </NuxtLink>
            </div>
        </div>
    </header>
</template>
<script>
import global from '~/mixins/global';
import axios from 'axios'
export default {
    mixins: [global],
    data() {
        return {
            hideHeaderOnPages: ['login', 'register'],
            isAuth: true,
            menuOpen: false,
            pathUrl: 'https://easyhelp.kz',
            userBalance: null,
            accountType: '',
        }
    },
    methods: {
        getBuyer() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/buyer-lk`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    this.userBalance = response.data.balance

                })
                .catch(error => console.log(error));
        },
        getSeller() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/seller/seller-lk`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios
                .get(path)
                .then(response => {
                    this.userBalance = response.data.balance

                })
                .catch(error => console.log(error));
        },

    },
    mounted() {
        const accType = localStorage.getItem('accountType')
        if (accType == 'buyer-account') {
            this.getBuyer()
            this.accountType = 'buyer'
            setInterval(() => {
                this.cartLength = localStorage.getItem('cartLength')
            }, 1);
        }
        else if (accType == 'seller-account') {
            this.getSeller()
            this.accountType = 'seller'
        }
        else {
            console.log('not authorized')
        }

    }
}
</script>
<style lang="scss" scoped>
header {
    padding: 40px 100px 30px;
    background: #fff;
    position: fixed;
    z-index: 100;
    width: 100%;

    @media (max-width: 1600px) {
        padding: 40px 50px 30px;
    }

    @media (max-width: 1024px) {
        padding: 40px 20px 30px;
    }

    .active {
        transform: translateX(0) !important;
    }

    .mobmenu {
        display: none;
        background: #8BBAFF;
        width: 100vw;
        height: 100vh;
        position: fixed;
        top: 0;
        left: 0;
        transform: translateX(100%);

        transition: all .3s ease;

        @media (max-width: 1024px) {
            display: flex;
            flex-direction: column;
            gap: 50px;

            justify-content: center;
            align-items: center;
        }

        .links {
            display: flex;
            flex-direction: column;
            gap: 31px;

            a {
                font-size: 32px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                font-family: var(--ral);
                color: #fff;
                text-decoration: none;
                text-align: left;
            }

            &:last-child {
                a {
                    margin-left: -40px;
                }
            }

            .refill {
                display: flex;
                align-items: center;
                gap: 20%;
                white-space: nowrap;
            }
        }
    }

    .header__body {
        display: flex;
        justify-content: space-between;
        align-items: center;

        .logopc {
            @media (max-width: 1024px) {
                display: none;
            }
        }

        .logomob {
            display: none;

            @media (max-width: 1024px) {
                display: block;
            }
        }

        .leftside {
            @media (max-width: 1024px) {
                display: none;
            }
        }

        div {
            display: flex;
            align-items: center;
            gap: 30px;

            &:last-child {
                gap: 20px;
            }

            .balance,
            .cash {
                @media (max-width: 1024px) {
                    display: none !important;

                }
            }

            .burg {
                display: none;

                @media (max-width: 1024px) {
                    display: block;
                }
            }

            span {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                font-family: var(--ral);
                color: #000;
            }

            a {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                font-family: var(--ral);
                color: #000;
                text-decoration: none;
            }
        }
    }
}

#menu__toggle {
    opacity: 0;
}

.menu__btn {
    margin-top: 10px;
    display: flex;
    /* используем flex для центрирования содержимого */
    align-items: center;
    /* центрируем содержимое кнопки */
    width: 35px;
    height: 20px;
    cursor: pointer;
    z-index: 100000000;
    color: #fff;
    position: relative;
    transform: rotate(180deg);
}

.menu__btn>span {
    display: block;
    position: absolute;
    width: 100%;
    height: 2px;
    background-color: #000;
}

.menu__btn>span::before,
.menu__btn>span::after {
    display: block;
    position: absolute;
    width: 100%;
    height: 2px;
    background-color: #000;
}

.menu__btn>span::before {
    content: '';
    top: -8px;
}

.menu__btn>span::after {
    content: '';
    top: 8px;
}

#menu__toggle:checked~.menu__btn>span {
    transform: rotate(45deg);
    background-color: #000;
    border-radius: 10px;

}

#menu__toggle:checked~.menu__btn>span::before {
    top: 0;
    transform: rotate(0);
    background-color: #000;
    border-radius: 10px;

}

#menu__toggle:checked~.menu__btn>span::after {
    top: 0;
    transform: rotate(90deg);
    background-color: #000;
    border-radius: 10px;
}

#menu__toggle:checked~.menu__box {
    visibility: visible;
    top: 0;
}

.menu__btn>span,
.menu__btn>span::before,
.menu__btn>span::after {
    transition-duration: .25s;
}
</style>