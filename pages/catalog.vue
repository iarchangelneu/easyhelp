<template>
    <div class="catalog">
        <h1>Каталог услуг</h1>

        <div class="filters">
            <div class="input-group">
                <input type="text" class="form-control" placeholder="Поиск" aria-label="search" v-model="search"
                    aria-describedby="basic-addon1">
                <div class="input-group-prepend">
                    <span class="input-group-text" id="basic-addon1">
                        <img src="@/assets/img/search.svg" alt="">
                    </span>
                </div>
            </div>
            <div class="buttons">
                <button @click="filter = !filter" :class="{ activeFil: filter }">
                    <span>Фильтр</span>
                    <img src="@/assets/img/filter.svg" alt="" :class="{ activeImg: filter }">
                </button>
                <button @click="sort = !sort" :class="{ activeFil: sort }">
                    <span>Сортировать</span>
                    <img src="@/assets/img/filter.svg" alt="" :class="{ activeImg: sort }">
                </button>
            </div>
        </div>

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
                    <NuxtLink to="/product/1">Подробнее</NuxtLink>
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
                    <NuxtLink to="/product/1">Подробнее</NuxtLink>
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
                    <NuxtLink to="/product/1">Подробнее</NuxtLink>
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
                    <NuxtLink to="/product/1">Подробнее</NuxtLink>
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
                    <NuxtLink to="/product/1">Подробнее</NuxtLink>
                </div>
            </div>
        </div>

        <div class="text-right">
            <button>Посмотреть все</button>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            search: '',
            sort: false,
            filter: false,
        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Каталог услуг | EasyHelp',
    ogTitle: 'Каталог услуг | EasyHelp',
    description: 'Каталог услуг | EasyHelp',
    ogDescription: 'Каталог услуг | EasyHelp',
})
</script>
<style lang="scss" scoped>
.catalog {
    padding: 150px 100px 80px;

    @media (max-width: 1600px) {
        padding: 150px 50px 80px;
    }

    @media (max-width: 1024px) {
        padding: 150px 20px 60px;
    }

    .text-right {
        margin-top: 30px;

        @media (max-width: 1024px) {
            text-align: center !important;
            margin-top: 20px;
        }

        button {
            padding: 10px 20px;
            background: transparent;
            border: 2px solid var(--btn);
            border-radius: 20px;

            font-size: 20px;
            font-style: normal;
            font-weight: 600;
            line-height: 130%;
            font-family: var(--ral);
            color: var(--btn);

            transition: all .3s ease;

            @media (max-width: 1024px) {
                font-size: 16px;
            }

            &:hover {
                color: #fff;
                background: var(--btn);
            }
        }
    }

    .catalog {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
        gap: 30px;
        grid-auto-flow: dense;
        padding: 0;
        margin-top: 30px;

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

    .filters {
        display: flex;
        gap: 30px;

        @media (max-width: 1024px) {
            flex-direction: column;
            gap: 20px;
        }

        .buttons {
            display: flex;
            gap: 30px;

            @media (max-width: 1024px) {
                gap: 0;
                display: flex;
                justify-content: space-between;
            }
        }

        .activeFil {
            background: var(--btn);
        }

        .activeImg {
            transform: rotate(90deg);
        }

        button {
            padding: 10px 20px;
            display: flex;
            gap: 7px;
            align-items: center;
            background: #8BBAFF;
            border-radius: 10px;
            border: 0;

            font-size: 20px;
            font-style: normal;
            font-weight: 600;
            line-height: 130%;
            font-family: var(--ral);
            color: #fff;
            transition: all .3s ease;

            img {
                transition: all .3s ease;
            }

            @media (max-width: 380px) {
                font-size: 16px;
            }
        }

        input {
            background: transparent;
            padding: 10px 20px;
            border-radius: 10px;
            border: 1px solid #E3E3E3;
            border-right: 0;
            border-top-right-radius: 0;
            border-bottom-right-radius: 0;
            height: 46px;
            box-shadow: none;

            font-size: 20px;
            font-style: normal;
            font-weight: 500;
            line-height: 130%;
            font-family: var(--ral);
            color: #000;

            &::placeholder {
                color: #000;
            }
        }

        .input-group {
            max-width: 770px;
        }

        .input-group-text {
            background: transparent;
            border-radius: 10px;
            border: 1px solid #E3E3E3;
            padding: 3px 20px 3px 5px;
            border-left: 0;
            border-top-left-radius: 0;
            border-bottom-left-radius: 0;
            height: 46px;
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
    }
}
</style>