<template>
    <div class="page">
        <PrevPage></PrevPage>

        <h1>Подтверждение заказа</h1>

        <div class="cart__body">
            <div class="cart__items">
                <div class="cart__item" v-if="cart.length > 0" v-for="item in cart" :key="item.id">
                    <img :src="pathUrl + '/api' + item.products.add_image[0].image" alt="">

                    <div class="item__info">
                        <h2>{{ item.products.name }}</h2>
                        <h2>{{ item.products.price.toLocaleString() + ' ₸' }}</h2>

                        <div class="text-right">
                            <img src="@/assets/img/delete.svg" @click="deleteFromCart(item.id)" alt="">
                        </div>
                    </div>
                </div>
            </div>


            <div class="complete">
                <h1>Подтверждение покупки</h1>
                <span>Количество заказов: {{ cart.length }}</span>
                <span>Итоговая сумма: {{ formatPrice(calculateTotal()) }} ₸ </span>
                <small>Сумма будет списана с вашего счета. Товары отобразятся во вкладке «Мои заказы» в Вашем Личном
                    кабинете.</small>

                <button @click="buyProduct()" ref="buyBtn">Подтвердить заказ</button>
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
            cart: [],
            pathUrl: 'https://easyhelp.kz',
        }
    },
    methods: {
        increment(item) {
            item.amount++;
            console.log(item)
            this.changeAmount(item)
        },
        decrement(item) {
            if (item.amount > 0) {
                item.amount--;
                console.log(item)
                this.changeAmount(item)
            }
            if (item.amount <= 0) {
                item.amount = 1
                this.deleteFromCart(item.id)
            }
        },
        buyProduct() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/placed-basket`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            this.$refs.buyBtn.innerHTML = 'Оформляем'
            axios
                .get(path)
                .then(response => {
                    console.log(response)
                    if (response.status == 204) {
                        this.$refs.buyBtn.innerHTML = 'Недостаточно средств'
                    }
                    if (response.status == 201) {
                        // this.getBuyer()
                        this.$refs.buyBtn.innerHTML = 'Оплата прошла успешно'

                        setTimeout(() => {
                            window.location.href = `/catalog`
                        }, 3);

                    }
                })
                .catch(error => {
                    console.error(error)
                })

        },
        changeAmount(item) {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/all-product-basket`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;

            axios
                .put(path, item)
                .then((res) => {
                    console.log(res)
                    //     this.getCart()
                })
                .catch((error) => {
                    console.error(error);

                });
        },
        calculateTotal() {
            let total = 0;

            this.cart.forEach(item => {
                const { price, discount } = item.products;
                const discountedPrice = price * (1 - discount / 100);
                total += discountedPrice * item.amount;
            });

            return total;
        },
        formatPrice(price) {
            return price.toLocaleString('ru-RU');
        },
        deleteFromCart(id) {
            const token = this.getAuthorizationCookie()
            const csrf = this.getCSRFToken()
            const path = `${this.pathUrl}/api/buyer/delete-product-basket/${id}`
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;
            axios.defaults.headers.common['X-CSRFToken'] = csrf;
            axios
                .put(path)
                .then(response => {
                    console.log(response)
                    this.getCart()
                })
                .catch(error => {
                    console.error(error)
                })
        },
        getCart() {
            const token = this.getAuthorizationCookie()
            const path = `${this.pathUrl}/api/buyer/all-product-basket`;
            axios.defaults.headers.common['Authorization'] = `Token ${token}`;

            axios
                .get(path)
                .then(response => {
                    this.cart = response.data
                })
                .catch(error => {
                    console.error(error)
                })
        },
    },
    mounted() {
        this.getCart()
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Подтверждение покупки | EasyHelp',
    ogTitle: 'Подтверждение покупки | EasyHelp',
    description: 'Подтверждение покупки | EasyHelp',
    ogDescription: 'Подтверждение покупки | EasyHelp',
})
</script>
<style lang="scss" scoped>
.page {
    padding: 150px 100px 90px;

    @media (max-width: 1600px) {
        padding: 150px 50px 90px;
    }

    @media (max-width: 1024px) {
        padding: 150px 20px 50px;
    }

    .cart__body {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        gap: 30px;

        @media (max-width: 1024px) {
            flex-direction: column;
            gap: 20px;
        }

        .complete {
            h1 {
                font-size: 32px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--ral);
                color: #000;
                margin: 0 0 30px;

                @media (max-width: 1024px) {
                    font-size: 16px;
                }
            }

            span {
                display: block;
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--ral);
                color: #000;
                margin: 0 0 20px;

                @media (max-width: 1024px) {
                    font-size: 16px;
                }
            }

            small {
                display: block;
                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--ral);
                color: #000;
                margin: 0 0 30px;
                max-width: 485px;
            }

            button {
                padding: 12px 4.427vw;
                background: transparent;
                border-radius: 20px;
                border: 2px solid var(--btn);

                color: var(--btn);
                font-family: var(--ral);
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;

                @media (max-width: 1024px) {
                    font-size: 16px;
                    padding: 12px 0;
                    width: 100%;
                }

                transition: all .3s ease;

                &:hover {
                    background: var(--btn);
                    color: #fff;
                }
            }
        }

        .cart__items {
            display: flex;
            flex-direction: column;
            gap: 30px;

            @media (max-width: 1024px) {
                gap: 20px;
                width: 100%;
            }

            .cart__item {
                border: 1px solid #E3E3E3;
                background: #F6FAFF;
                padding: 20px;
                max-width: 600px;

                @media (max-width:1024px) {
                    max-width: 100%;
                    width: 100%;
                    gap: 10px;
                }

                display: flex;
                gap: 20px;



                .item__info {
                    display: flex;
                    flex-direction: column;
                    gap: 20px;
                    width: 100%;

                    h2 {
                        font-size: 20px;
                        font-style: normal;
                        font-weight: 600;
                        line-height: 130%;
                        font-family: var(--ral);
                        color: #000;

                        @media (max-width: 1024px) {
                            font-size: 16px;
                        }
                    }

                    .text-right {
                        margin-top: auto;

                        img {
                            width: 40px;
                            height: 40px;
                            cursor: pointer;
                        }
                    }
                }

                img {
                    width: 200px;
                    height: 200px;
                    object-fit: cover;

                    @media (max-width: 1024px) {
                        width: 100px;
                        height: 100px;
                    }
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
        margin: 10px 0 30px;

        @media (max-width: 1024px) {
            font-size: 20px;
            margin: 10px 0 20px;
        }
    }
}
</style>