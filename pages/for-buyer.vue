<template>
    <div class="page">
        <h1>О платформе</h1>

        <div class="about">
            <div class="left">
                <div class="links">
                    <NuxtLink to="/for-buyer">Я заказчик</NuxtLink>
                    <img src="@/assets/img/aboutline2.svg" alt="">
                    <NuxtLink to="/for-seller">Я исполнитель</NuxtLink>
                </div>

                <p>Добро пожаловать в EasyHelp.kz – надёжного партнёра для всех вопросов, связанных с уходом за домом.
                    Мы с гордостью предоставляем широкий спектр услуг, обеспечивая вашему жилищу безупречную ухоженность
                    и комфорт.</p>
                <p>Что мы предлагаем?</p>

                <ul>
                    <li>Клининг и уборка: наша команда умеет придать дому бриллиантовую чистоту. Мы используем современные
                        методы и экологически чистые средства для уборки, чтобы обеспечить безопасность вашей семьи.</li>
                    <li>Ремонт и обновление: если вашему дому требуется обновление или ремонт, EasyHelp.kz готова взять
                        на себя эту задачу. Мы осуществляем ремонтные работы любой сложности, соблюдая высокие стандарты
                        качества.</li>
                    <li>Сантехнические услуги: проблемы с водоснабжением или сантехникой могут быть довольно беспокойными.
                        Наши профессиональные сантехники приходят на помощь, чтобы устранить неполадки и обеспечить
                        правильное функционирование ваших систем.</li>
                </ul>

                <p>В EasyHelp.kz, мы придерживаемся ценностей, которые делают нас лучшими в своей области. Надёжность,
                    качество и внимание к деталям — это то, что мы приносим в каждый проект. Мы гордимся нашей способностью
                    предоставлять услуги, которые улучшают качество жизни клиентов.</p>

                <p>Почему выбирают нас?</p>

                <ul>
                    <li>Профессиональные специалисты: наши сотрудники обладают большим опытом и прошли обучение,
                        чтобы обеспечить наивысший стандарт услуг.</li>
                    <li>Подход к клиенту: мы слушаем ваши потребности и предоставляем решения, которые соответствуют вашим
                        ожиданиям.</li>
                    <li>Прозрачность и надёжность: мы ценим ваше доверие и всегда соблюдаем согласованные сроки и бюджет.
                    </li>
                    <li>Экологически чистые методы: мы заботимся о вашем здоровье и окружающей среде, используя безопасные
                        и экологически чистые средства.</li>
                </ul>

                <p>Мы гордимся тем, что помогаем нашим клиентам сделать их дома лучше. Пригласите EasyHelp.kz в свой дом,
                    и мы уверены, что вы останетесь довольны результатом.</p>

                <NuxtLink to="/register" class="reg">Регистрация</NuxtLink>
            </div>

            <div class="right">
                <img src="@/assets/img/stage1.png" class="img-fluid" alt="">
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
    title: 'Для Заказчика | EasyHelp',
    ogTitle: 'Для Заказчика | EasyHelp',
    description: 'Для Заказчика | EasyHelp',
    ogDescription: 'Для Заказчика | EasyHelp',
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

    .about {
        display: flex;
        gap: 60px;
        align-items: flex-start;

        .right {
            margin-top: 50px;

            @media (max-width: 1024px) {
                display: none;
            }
        }

        .left {
            .reg {
                display: inline-block;
                padding: 10px 20px;
                background: transparent;
                border-radius: 10px;
                border: 2px solid var(--btn);
                margin-top: 30px;

                font-size: 20px;
                font-style: normal;
                font-weight: 600;
                line-height: 130%;
                font-family: var(--ral);
                color: var(--btn);
                text-decoration: none;

                transition: all .3s ease;

                &:hover {
                    background: var(--btn);
                    color: #fff;
                }
            }

            ul {
                padding: 0 0 0 20px;
            }

            p,
            li {
                margin: 0 0 10px;
                max-width: 1070px;

                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--ral);
                color: #000;
            }

            .links {
                display: flex;
                gap: 15px;
                margin: 0 0 20px;

                a {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: 130%;
                    font-family: var(--ral);
                    color: var(--btn);
                    text-decoration: none;

                    &:last-child {
                        color: #000;
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
        margin: 0 0 30px;

        @media (max-width: 1024px) {
            font-size: 20px;
        }
    }
}
</style>