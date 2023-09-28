<template>
    <div class="page">
        <PrevPage></PrevPage>

        <h1>Подтверждение заказа</h1>

        <div class="cart__body">
            <div class="cart__items">
                <div class="cart__item">
                    <img src="@/assets/img/cart.png" alt="">

                    <div class="item__info">
                        <h2>Услуга Установка сантехники</h2>
                        <h2>80 000 ₸</h2>

                        <div class="text-right">
                            <img src="@/assets/img/delete.svg" alt="">
                        </div>
                    </div>
                </div>
                <div class="cart__item">
                    <img src="@/assets/img/cart.png" alt="">

                    <div class="item__info">
                        <h2>Услуга Установка сантехники</h2>
                        <h2>80 000 ₸</h2>

                        <div class="text-right">
                            <img src="@/assets/img/delete.svg" alt="">
                        </div>
                    </div>
                </div>
            </div>


            <div class="complete">
                <h1>Подтверждение покупки</h1>
                <span>Количество заказов: 2</span>
                <span>Итоговая сумма: 156 000 ₸ </span>
                <small>Сумма будет списана с вашего счета. Товары отобразятся во вкладке «Мои заказы» в Вашем Личном
                    кабинете.</small>

                <button>Подтвердить заказ</button>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {}
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