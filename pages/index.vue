<template>
    <div class="page">

        <div class="main">
            <div class="main__body">
                <div class="main__left">
                    <h1>Профессионалы своего дела для вашего дома</h1>
                    <p>Надёжные исполнители, современное оборудование и эффективные методы гарантируют идеальный результат.
                        Доверьте нам заботу о доме, чтобы вы могли наслаждаться своим временем и работой без лишних забот
                    </p>
                    <div class="links">
                        <NuxtLink to="/catalog">Выбрать услугу</NuxtLink>
                        <NuxtLink to="/experts">Выбрать исполнителя</NuxtLink>
                    </div>
                </div>

                <img src="@/assets/img/ludi.png" class="trashak img-fluid" alt="">
            </div>
        </div>

        <div class="populars">
            <h1>Популярные услуги</h1>

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
                <NuxtLink to="/catalog">Посмотреть все</NuxtLink>
            </div>
        </div>

        <div class="about">
            <h1>О нас</h1>

            <div class="about__body">
                <div class="about__left">
                    <div class="area" v-if="isSeller">
                        <div class="links">
                            <span :class="{ activeSpan: isSeller }" @click="isSeller = true">Я заказчик</span>
                            <img src="@/assets/img/aboutline.svg" alt="">
                            <span :class="{ activeSpan: !isSeller }" @click="isSeller = false">Я исполнитель</span>
                        </div>
                        <p>
                            <span>EasyHelp.kz –</span>
                            это команда профессионалов, объединённых общей целью — сделать ваш дом идеальным местом
                            для жизни.
                            Наш опыт и страсть к качеству позволяют нам предоставлять услуги, которые вы заслуживаете.
                            Мы тщательно подходим к каждому проекту, будь то клининг, ремонт, сантехнические работы
                            или другие
                            услуги по дому.
                        </p>
                        <NuxtLink to="/for-seller">Подробнее</NuxtLink>
                    </div>
                    <div class="area" v-else>
                        <div class="links">
                            <span :class="{ activeSpan: isSeller }" @click="isSeller = true">Я заказчик</span>
                            <img src="@/assets/img/aboutline.svg" alt="">
                            <span :class="{ activeSpan: !isSeller }" @click="isSeller = false">Я исполнитель</span>
                        </div>
                        <p>
                            <span>EasyHelp.kz –</span>
                            это сообщество профессиональных исполнителей, каждый из которых обладает уникальными навыками и
                            страстью к своей работе. Мы предоставляем нашим специалистам возможность предложить свои услуги
                            широкой аудитории клиентов, которые ищут экспертов для решения различных задач в своих домах.
                        </p>
                        <NuxtLink to="/for-buyer">Подробнее</NuxtLink>
                    </div>
                </div>

                <img src="@/assets/img/about.png" v-if="isSeller" class="img-fluid" alt="">
                <img src="@/assets/img/about2.png" v-if="!isSeller" class="img-fluid" alt="">
            </div>
        </div>

        <div class="populars">
            <h1>Популярные исполнители</h1>

            <div class="catalog">
                <div class="catalog__item">
                    <img src="@/assets/img/exp1.png" alt="">
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
                    <img src="@/assets/img/exp2.png" alt="">
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
                    <img src="@/assets/img/exp3.png" alt="">
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
                    <img src="@/assets/img/exp4.png" alt="">
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
                    <img src="@/assets/img/exp5.png" alt="">
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

            <div class="text-right">
                <NuxtLink to="/experts">Посмотреть все</NuxtLink>
            </div>
        </div>

        <div class="reviews">
            <h1>Отзывы</h1>

            <div class="reviews__slider">
                <swiper :slides-per-view="3" :space-between="30" :breakpoints="breakpoints" :modules="modules"
                    :navigation="navigation2" class="ska">
                    <swiper-slide class="slide">
                        <h1>Содержу дом в порядке с EasyHelp.kz </h1>

                        <p>Я долго искала надежного специалиста для ремонта ванной комнаты, и мне посоветовали данный
                            сервис. Они быстро нашли подходящего ремонтника для моего проекта. Результат был потрясающим!
                            Ванная выглядит как новая, и я не могу быть счастливее. Отличная работа
                        </p>

                        <div class="text-right">
                            <small>Марина</small>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <h1>Идеальный клининг</h1>

                        <p>Я обратилась сюда для клининга перед важным мероприятием. Команда была очень профессиональной и
                            добросовестной. Мой дом блестел, и все мои гости были в восторге. Большое спасибо за ваше
                            качество и надежность
                        </p>

                        <div class="text-right">
                            <small>Ирина</small>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <h1>Профи своего дела</h1>

                        <p>Помогли мне с сантехническими работами в моем доме. У меня не было нужного инструмента,
                            специалисты пришли вовремя, решили проблему оперативно и профессионально. Теперь у меня нет
                            никаких проблем с водоснабжением. Очень рекомендую их услуги
                        </p>

                        <div class="text-right">
                            <small>Николай</small>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <h1>Содержу дом в порядке с EasyHelp.kz </h1>

                        <p>Я долго искала надежного специалиста для ремонта ванной комнаты, и мне посоветовали данный
                            сервис. Они быстро нашли подходящего ремонтника для моего проекта. Результат был потрясающим!
                            Ванная выглядит как новая, и я не могу быть счастливее. Отличная работа
                        </p>

                        <div class="text-right">
                            <small>Марина</small>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <h1>Идеальный клининг</h1>

                        <p>Я обратилась сюда для клининга перед важным мероприятием. Команда была очень профессиональной и
                            добросовестной. Мой дом блестел, и все мои гости были в восторге. Большое спасибо за ваше
                            качество и надежность
                        </p>

                        <div class="text-right">
                            <small>Ирина</small>
                        </div>
                    </swiper-slide>
                    <swiper-slide class="slide">
                        <h1>Профи своего дела</h1>

                        <p>Помогли мне с сантехническими работами в моем доме. У меня не было нужного инструмента,
                            специалисты пришли вовремя, решили проблему оперативно и профессионально. Теперь у меня нет
                            никаких проблем с водоснабжением. Очень рекомендую их услуги
                        </p>

                        <div class="text-right">
                            <small>Николай</small>
                        </div>
                    </swiper-slide>
                </swiper>
                <div class="navs">
                    <img src="@/assets/img/prev.svg" alt="" class="prev">
                    <img src="@/assets/img/next.svg" alt="" class="next">
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import { Navigation } from 'swiper/modules';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';
export default {
    data() {
        return {
            isSeller: true,
            modules: [Navigation],
            navigation2: {
                nextEl: '.next',
                prevEl: '.prev',
            },

            breakpoints: {
                320: {
                    slidesPerView: 'auto',
                    spaceBetween: 20,

                },
                1025: {
                    slidesPerView: 3,
                    spaceBetween: 30,
                }
            },
        }
    },
}
</script>
<script setup>
useSeoMeta({
    title: 'Главная | EasyHelp',
    ogTitle: 'Главная | EasyHelp',
    description: 'Главная | EasyHelp',
    ogDescription: 'Главная | EasyHelp',
})
</script>
<style lang="scss" scoped>
.page {
    padding: 120px 100px 80px;

    @media (max-width: 1600px) {
        padding: 120px 50px 80px;
    }

    @media (max-width: 1024px) {
        padding: 120px 20px 30px;
    }

    .reviews {

        .navs {
            @media (max-width: 1024px) {
                display: flex;
                gap: 10px;
                justify-content: flex-end;
                width: 100%;
            }

            .prev {
                display: none;

                @media (max-width: 1024px) {
                    display: block;
                }
            }
        }

        .reviews__slider {
            display: flex;
            align-items: center;
            gap: 10px;

            @media (max-width: 1024px) {
                flex-direction: column;
            }

            img {
                cursor: pointer;
            }

            .ska {
                @media (max-width: 1024px) {
                    width: 100%;
                }
            }

            .slide {
                border: 1px solid #E3E3E3;
                background: #F6FAFF;
                padding: 20px;
                display: flex;
                flex-direction: column;
                height: 210px;

                @media (max-width: 1024px) {
                    width: 100%;
                }

                h1 {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 600;
                    line-height: 130%;
                    font-family: var(--ral);
                    color: var(--btn);

                    margin: 0 0 10px;

                    @media (max-width: 1024px) {
                        font-size: 16px;
                        //  max-width: 100;
                    }
                }

                p {
                    font-size: 16px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--ral);
                    color: #000;

                    @media (max-width: 1024px) {
                        //   max-width: 330px;
                        font-size: 12px;
                    }
                }

                .text-right {
                    margin-top: auto;

                    @media (max-width: 1024px) {
                        //   max-width: 330px;
                    }

                    small {
                        font-size: 16px;
                        font-style: normal;
                        font-weight: 600;
                        line-height: 130%;
                        font-family: var(--ral);
                        color: #000;


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
            margin: 50px 0 30px;

            @media (max-width: 1024px) {
                font-size: 20px;
                margin: 30px 0 20px;
            }
        }
    }

    .about {
        .about__body {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 57px 163px 57px 60px;
            border-radius: 100px 0px;
            background: #8BBAFF;

            @media (max-width: 1400px) {
                padding: 57px 60px;
            }

            @media (max-width: 1024px) {
                padding: 30px 20px;
                border-radius: 20px;

                flex-direction: column;
            }

            .about__left {

                @media (max-width: 1024px) {
                    margin-bottom: 40px;
                }

                .area {
                    max-width: 790px;

                    p {
                        margin: 20px 0 30px;
                        font-size: 20px;
                        font-style: normal;
                        font-weight: 500;
                        line-height: 130%;
                        font-family: var(--ral);
                        color: #fff;

                        @media (max-width: 1024px) {
                            font-size: 16px;
                        }

                        span {
                            font-weight: 700;
                        }
                    }

                    a {
                        padding: 10px 20px;
                        background: #fff;
                        border-radius: 20px;
                        //  border: 2px solid #fff;
                        text-decoration: none;

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
                            background: var(--btn);
                            color: #fff;
                        }
                    }
                }

                .links {
                    display: flex;
                    gap: 13px;

                    @media (max-width: 1024px) {
                        justify-content: center;
                    }

                    .activeSpan {
                        color: var(--btn) !important;
                    }

                    span {
                        font-size: 20px;
                        font-style: normal;
                        font-weight: 500;
                        line-height: 130%;
                        font-family: var(--ral);
                        color: #fff;

                        transition: all .3s ease;
                        cursor: pointer;
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
            margin: 50px 0 30px;

            @media (max-width: 1024px) {
                font-size: 20px;
                margin: 30px 0 20px;
            }
        }
    }

    .populars {

        .text-right {
            margin-top: 30px;

            @media (max-width: 1024px) {
                text-align: center !important;
            }

            a {
                padding: 10px 20px;
                background: transparent;
                border-radius: 20px;
                text-decoration: none;
                display: inline-block;
                border: 2px solid var(--btn);

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
                    background: var(--btn);
                    color: #fff;
                }
            }
        }

        .catalog {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 30px;
            grid-auto-flow: dense;

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

        h1 {
            font-size: 40px;
            font-style: normal;
            font-weight: 600;
            line-height: 130%;
            font-family: var(--ral);
            color: #000;
            margin: 50px 0 30px;

            @media (max-width: 1024px) {
                font-size: 20px;
                margin: 30px 0 20px;
            }
        }
    }

    .main__body {
        border-radius: 100px 0px;
        background: #8BBAFF;
        padding: 0 0 0 40px;

        display: flex;
        align-items: center;
        justify-content: space-between;

        @media (max-width: 1024px) {
            flex-direction: column;
            padding: 30px 40px 0 20px;
            border-radius: 20px;
        }

        .trashak {
            @media (max-width: 1600px) {
                max-width: 46.458vw;
            }

            @media (max-width: 1024px) {
                max-width: 100%;
            }
        }

        .main__left {
            max-width: 788px;

            h1 {
                font-size: 64px;
                font-style: normal;
                font-weight: 600;
                line-height: 130%;
                font-family: var(--ral);
                color: #fff;
                margin: 0 0 20px;

                @media (max-width: 1600px) {
                    line-height: 100%;
                }

                @media (max-width: 1400px) {
                    font-size: 32px;
                }

                @media (max-width: 1024px) {
                    line-height: 130%;
                    margin: 0 0 10px;
                }
            }

            p {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--ral);
                color: #fff;
                margin: 0 0 30px;

                @media (max-width: 1400px) {
                    font-size: 16px;
                }
            }

            .links {
                display: flex;
                gap: 30px;

                @media (max-width: 1024px) {
                    flex-direction: column;
                    gap: 20px;
                    align-items: flex-start;
                    margin-bottom: 25px;
                }

                a {
                    border-radius: 20px;
                    background: #fff;
                    text-decoration: none;
                    padding: 10px 20px;
                    border: 2px solid transparent;

                    font-size: 20px;
                    font-style: normal;
                    font-weight: 600;
                    line-height: 130%;
                    font-family: var(--ral);
                    color: var(--btn);

                    transition: all .3s ease;

                    @media (max-width: 1400px) {
                        font-size: 16px;
                    }

                    &:hover {
                        background: transparent;
                        border: 2px solid var(--btn);
                    }
                }
            }
        }
    }
}
</style>