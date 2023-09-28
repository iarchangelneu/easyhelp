<template>
    <div class="product">
        <prevPage></prevPage>

        <h1>Услуга Генеральная уборка</h1>


        <div class="product__info">
            <div class="image">
                <img src="@/assets/img/product.png" alt="">

                <div class="category">
                    <h2>Категория: <span>клининг</span></h2>

                    <ul>
                        <li>Мытье окон</li>
                        <li>Чистка сантехники</li>
                        <li>Мытье полов с отпариванием</li>
                        <li>1 раз в неделю</li>
                    </ul>
                </div>
            </div>

            <div class="product__desc">
                <h3>Пакетое предложение, уборка раз в неделю в течение месяца</h3>
                <h2>Описание услуги:</h2>

                <div v-html="description" class="description"></div>
                <div class="mobauthor">
                    <div class="author">
                        <span>Автор: <NuxtLink to="/expert/1">Клининг «Белоснежка»</NuxtLink></span>
                        <span style="display: flex; align-items: center; gap: 17px;">Рейтинг: 4,5 <img
                                src="@/assets/img/star.svg" alt=""></span>
                        <span>Количество услуг на сайте: 6</span>
                    </div>
                </div>
                <div class="price">
                    <span>80 000 ₸</span>
                    <button>Заказать</button>
                </div>
            </div>

            <div class="product__author">
                <div class="author">
                    <span>Автор: <NuxtLink to="/expert/1">Клининг «Белоснежка»</NuxtLink></span>
                    <span style="display: flex; align-items: center; gap: 17px;">Рейтинг: 4,5 <img
                            src="@/assets/img/star.svg" alt=""></span>
                    <span>Количество услуг на сайте: 6</span>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            description: 'Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание',
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