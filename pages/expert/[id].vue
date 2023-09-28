<template>
    <div class="expert">
        <prevPage></prevPage>

        <h1>Клининг «Белоснежка»</h1>

        <div class="expert__info">
            <img src="@/assets/img/expert.png" alt="">

            <div class="expert__desc">
                <h2>Категория: <span>клининг</span></h2>

                <h2>Описание услуги:</h2>

                <div v-html="description"></div>
            </div>

            <div class="expert__tags">
                <ul>
                    <li>Разные виды площади</li>
                    <li>Выгодный прайс</li>
                    <li>Экологичные средства</li>
                    <li>Сложные виды уборки</li>
                </ul>
            </div>
        </div>

        <div class="expert__catalog">
            <h1>Услуги исполнителя</h1>

            <div class="catalog">
                <div class="catalog__item">
                    <img src="@/assets/img/pop1.png" alt="">
                    <h1>Генеральная уборка</h1>

                    <ul>
                        <li>Мытье окон</li>
                        <li>Чистка сантехники</li>
                        <li>Мытье полов с отпариванием</li>
                        <li>1 раз в неделю</li>
                    </ul>

                    <div class="price">
                        <h2>80 000 ₸</h2>
                        <NuxtLink to="/expert/1">Подробнее</NuxtLink>
                    </div>
                </div>
                <div class="catalog__item">
                    <img src="@/assets/img/pop5.png" alt="">
                    <h1>Генеральная уборка</h1>

                    <ul>
                        <li>Мытье окон</li>
                        <li>Чистка сантехники</li>
                        <li>Мытье полов с отпариванием</li>
                    </ul>

                    <div class="price">
                        <h2>80 000 ₸</h2>
                        <NuxtLink to="/expert/1">Подробнее</NuxtLink>
                    </div>
                </div>
                <div class="catalog__item">
                    <img src="@/assets/img/pop2.png" alt="">
                    <h1>Генеральная уборка</h1>

                    <ul>
                        <li>Мытье окон</li>
                        <li>Чистка сантехники</li>
                        <li>Мытье полов с отпариванием</li>
                        <li>1 раз в неделю</li>
                    </ul>

                    <div class="price">
                        <h2>80 000 ₸</h2>
                        <NuxtLink to="/expert/1">Подробнее</NuxtLink>
                    </div>
                </div>
                <div class="catalog__item">
                    <img src="@/assets/img/pop3.png" alt="">
                    <h1>Генеральная уборка</h1>

                    <ul>
                        <li>Мытье окон</li>
                        <li>Чистка сантехники</li>
                        <li>Мытье полов с отпариванием</li>
                        <li>1 раз в неделю</li>
                    </ul>

                    <div class="price">
                        <h2>80 000 ₸</h2>
                        <NuxtLink to="/expert/1">Подробнее</NuxtLink>
                    </div>
                </div>
                <div class="catalog__item">
                    <img src="@/assets/img/pop4.png" alt="">
                    <h1>Генеральная уборка</h1>

                    <ul>
                        <li>Мытье окон</li>
                        <li>Чистка сантехники</li>
                        <li>Мытье полов с отпариванием</li>
                        <li>1 раз в неделю</li>
                    </ul>

                    <div class="price">
                        <h2>80 000 ₸</h2>
                        <NuxtLink to="/expert/1">Подробнее</NuxtLink>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            description: 'Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание Тут будет описание',
        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Исполнитель | EasyHelp',
    ogTitle: 'Исполнитель | EasyHelp',
    description: 'Исполнитель | EasyHelp',
    ogDescription: 'Исполнитель | EasyHelp',
})
</script>
<style lang="scss" scoped>
.expert {
    padding: 150px 100px 80px;

    @media (max-width: 1600px) {
        padding: 150px 50px 80px;
    }

    @media (max-width: 1024px) {
        padding: 150px 20px 60px;
    }

    .expert__catalog {
        h1 {
            font-size: 24px;
            font-style: normal;
            font-weight: 600;
            line-height: 130%;
            font-family: var(--ral);
            color: #000;
            margin: 30px 0;

            @media (max-width: 1024px) {
                font-size: 20px;
                margin: 20px 0;
            }
        }

        .catalog {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 30px;
            grid-auto-flow: dense;
            padding: 0;

            @media (max-width: 1024px) {
                gap: 20px;
                padding: 0 15px;
            }

            @media (max-width: 380px) {
                padding: 0;
            }

            .catalog__item {
                width: 100%;
                display: flex;
                flex-direction: column;
                padding: 20px;
                gap: 10px;

                border: 1px solid #E3E3E3;
                background: #F6FAFF;


                img {
                    width: 100%;
                    height: 280px;
                    object-fit: cover;
                }

                h1 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 600;
                    line-height: 130%;
                    font-family: var(--ral);
                    color: #000;
                    margin: 0 !important;
                }

                ul {
                    padding: 0 0 0 20px;
                    margin: 0;

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

                .price {
                    display: flex;
                    gap: 40px;
                    align-items: center;
                    justify-content: space-between;
                    margin-top: auto;

                    h2 {
                        font-size: 20px;
                        font-style: normal;
                        font-weight: 600;
                        line-height: 130%;
                        font-family: var(--ral);
                        color: #000;
                        margin: 0;
                    }

                    a {
                        text-decoration: none;
                        padding: 10px;
                        background: transparent;
                        border-radius: 20px;
                        border: 2px solid var(--btn);

                        font-size: 20px;
                        font-style: normal;
                        font-weight: 500;
                        line-height: 130%;
                        font-family: var(--btn);
                        color: var(--btn);

                        transition: all .3s ease;

                        &:hover {
                            background: var(--btn);
                            color: #fff;
                        }
                    }
                }
            }
        }
    }

    .expert__info {
        display: flex;
        gap: 30px;
        width: 100%;

        @media (max-width: 1024px) {
            flex-direction: column;
            gap: 20px;
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

        .expert__tags {
            ul {
                padding: 0 0 0 20px;
                margin: 0;

                li {
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--ral);
                    color: #000;
                    margin-bottom: 10px;
                    white-space: nowrap;

                    &:last-child {
                        margin-bottom: 0;
                    }
                }
            }
        }

        .expert__desc {
            h2 {
                font-size: 20px;
                font-style: normal;
                font-weight: 600;
                line-height: 130%;
                font-family: var(--ral);
                color: #000;

                span {
                    font-weight: 500;
                }

                margin-bottom: 20px;

                &:last-child {
                    margin-bottom: 10px;
                }


            }

            div {
                max-width: 989px;
                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--var);
                color: #000;

                @media (max-width: 1600px) {
                    max-width: 700px;
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