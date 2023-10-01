<template>
    <div v-if="product.length <= 0"></div>
    <div class="product" v-else>
        <prevPage></prevPage>

        <h1> {{ product.name }}</h1>


        <div class="product__info">
            <div class="image">
                <img :src="product.add_image[0].image" alt="">

                <div class="category">
                    <h2>Категория: <span>{{ product.category.category_name }}</span></h2>

                    <ul v-if="product.key_features">
                        <li v-for="(feature, index) in product.key_features.split('\r\n')" :key="index">{{ feature }}
                        </li>
                    </ul>
                </div>
            </div>

            <div class="product__desc">

                <div v-html="product.description" class="description"></div>
                <div class="mobauthor">
                    <div class="author">
                        <span>Автор: <NuxtLink :to="'/expert/' + product.seller.id">{{ seller.first_name }}</NuxtLink>
                            </span>
                        <span style="display: flex; align-items: center; gap: 17px;">Рейтинг: {{ product.seller.rating }}
                            <img src="@/assets/img/star.svg" alt=""></span>
                        <span>Количество услуг на сайте: {{ product.seller.amount_products }}</span>
                    </div>
                </div>
                <div class="price">
                    <span>{{ product.price.toLocaleString() + ' ₸' }}</span>
                    <button ref="cartBtn" @click="addToCart()" v-if="accType == 'buyer' || accType == ''">Заказать</button>
                </div>
            </div>

            <div class="product__author">
                <div class="author">
                    <span>Автор: <NuxtLink :to="'/expert/' + product.seller.id">{{ seller.first_name }}</NuxtLink></span>
                    <span style="display: flex; align-items: center; gap: 17px;">Рейтинг: {{ product.seller.rating }} <img
                            src="@/assets/img/star.svg" alt=""></span>
                    <span>Количество услуг на сайте: {{ product.seller.amount_products }}</span>
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
            productId: this.$route.params.id,
            product: [],
            seller: [],
            pathUrl: 'https://easyhelp.kz',
            category: '',
            rating: null,
            count: null,
            apiResponse: '',
            accType: '',
            description: 'Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание',
        }
    },
    methods: {
        addToCart() {
            const path = `${this.pathUrl}/api/buyer/add-product-basket`
            const csrf = this.getCSRFToken()

            if (!this.accType == '') {

                axios.defaults.headers.common['X-CSRFToken'] = csrf;
                axios
                    .post(path, {
                        products: this.product.id,
                        amount: 1,
                    })
                    .then(response => {
                        if (response.status == 201) {
                            this.$refs.cartBtn.innerHTML = 'Добавлен в корзину'
                            this.$refs.cartBtn.disabled = true
                            this.$refs.cartBtn.classList.add('disabled')
                            this.getCart()
                        }
                        else {
                            this.$refs.cartBtn.innerHTML = 'Произошла ошибка, попробуйте еще раз'
                            this.$refs.cartBtn.disabled = false

                        }
                        console.log(response)
                    })
                    .catch(error => {
                        console.error(error)
                    })
            }
            else {
                window.location.href = '/login'
            }
        },

        getProduct() {
            const path = `${this.pathUrl}/api/products/detail-product/${this.productId}`
            axios
                .get(path)
                .then(response => {
                    this.product = response.data
                    this.seller = response.data.seller.user
                    this.rating = response.data.seller.rating
                    this.category = response.data.category.category_name
                    this.count = response.data.seller.amount_products
                })
                .catch(error => {
                    console.error(error)
                })
        },
    },
    mounted() {
        this.getProduct()

        const accType = localStorage.getItem('accountType')
        if (accType == 'buyer-account') {
            this.accType = 'buyer'
        }
        else if (accType == 'seller-account') {
            this.accType = 'seller'
        }
        else {
            this.accType = ''
            console.log('not authorized')
        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Услуга | EasyHelp',
    ogTitle: 'Услуга | EasyHelp',
    description: 'Услуга | EasyHelp',
    ogDescription: 'Услуга | EasyHelp',
})
</script>
<style lang="scss" scoped>
.product {
    padding: 150px 100px 80px;

    @media (max-width: 1600px) {
        padding: 150px 50px 80px;
    }

    @media (max-width: 1024px) {
        padding: 150px 20px 50px;
    }

    .product__info {
        display: flex;
        gap: 30px;
        width: 100%;

        @media (max-width: 1024px) {
            flex-direction: column;
            gap: 20px;
        }

        .product__author {
            @media (max-width: 1024px) {
                display: none;
            }

            .author {
                display: flex;
                flex-direction: column;
                gap: 10px;

                span {
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--ral);
                    color: #000;
                    white-space: nowrap;

                    a {
                        text-decoration: underline;
                        color: #000;
                    }
                }
            }
        }

        .product__desc {
            .mobauthor {
                margin-top: 20px;
                display: none;

                @media (max-width: 1024px) {
                    display: block;
                }

                .author {
                    display: flex;
                    flex-direction: column;
                    gap: 10px;

                    span {
                        font-size: 16px;
                        font-style: normal;
                        font-weight: 500;
                        line-height: 130%;
                        font-family: var(--ral);
                        color: #000;
                        white-space: nowrap;

                        a {
                            text-decoration: underline;
                            color: #000;
                        }
                    }
                }
            }

            .price {
                display: flex;
                gap: 30px;
                align-items: center;
                margin-top: 34px;

                span {
                    font-size: 36px;
                    font-style: normal;
                    font-weight: 600;
                    line-height: 130%;
                    font-family: var(--ral);
                    color: #000;
                    white-space: nowrap;
                }

                button {
                    background: transparent;
                    padding: 10px 20px;
                    border-radius: 20px;
                    border: 2px solid var(--btn);

                    font-size: 20px;
                    font-style: normal;
                    font-weight: 600;
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

            .description {
                max-width: 989px;
                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--ral);
                color: #000;
            }

            h2 {
                font-size: 20px;
                font-style: normal;
                font-weight: 600;
                line-height: 130%;
                font-family: var(--ral);
                color: #000;
                margin: 0 0 10px;
            }

            h3 {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--ral);
                color: #000;

                margin: 0 0 20px;
            }
        }

        .image {
            .category {
                ul {
                    margin: 0;
                    padding: 0 0 0 20px;

                    li {
                        font-size: 16px;
                        font-style: normal;
                        font-weight: 500;
                        line-height: 130%;
                        font-family: var(--ral);
                        color: #000;
                        margin-bottom: 10px;

                        &:last-child {
                            margin-bottom: 0;
                        }
                    }
                }

                h2 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 600;
                    line-height: 130%;
                    font-family: var(--ral);
                    color: #000;
                    margin: 20px 0;

                    span {
                        font-weight: 500;
                    }
                }
            }

            img {
                width: 18.229vw;
                height: 18.229vw;
                object-fit: cover;

                @media (max-width: 1024px) {
                    width: 100%;
                    height: 350px;
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