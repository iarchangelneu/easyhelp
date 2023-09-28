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

                <p>Добро пожаловать в EasyHelp.kz – новое пространство для профессиональных мастеров, готовых сделать дома
                    наших клиентов лучше. Мы гордимся тем, что объединяем опытных специалистов в области ремонта,
                    садоводства, сантехники, и других домашних услуг, предоставляя им платформу для роста и сотрудничества.
                </p>
                <p>Что мы предлагаем?</p>

                <ul>
                    <li>Расширение клиентской базы: присоединившись к EasyHelp.kz, вы получите доступ к новым клиентам и
                        широкой аудитории, ищущей профессиональные услуги.</li>
                    <li>Удобство и простота: платформа предоставляет удобные инструменты для управления заказами,
                        расписаниями и коммуникации с клиентами, делая вашу работу более организованной.</li>
                    <li>Поддержка и обучение: мы поддерживаем наших исполнителей, предоставляя обучение и ресурсы для
                        профессионального роста.</li>
                </ul>

                <p>В EasyHelp.kz, мы придерживаемся ценностей, которые делают нас лучшими в своей области. Надёжность,
                    качество и внимание к деталям — это то, что мы приносим в каждый проект. Мы гордимся нашей способностью
                    предоставлять услуги, которые улучшают качество жизни наших клиентов.</p>

                <p>Почему выбирают нас?</p>

                <ul>
                    <li>Профессиональные возможности: мы предоставляем платформу, на которой вы можете продемонстрировать
                        навыки и найти клиентов, которые оценят вашу работу.</li>
                    <li>Сотрудничество: мы поощряем сотрудничество и обмен опытом между специалистами, чтобы помочь вам
                        стать лучше.</li>
                    <li>Рост бизнеса: мы помогаем исполнителям расширять свой бизнес и привлекать больше клиентов.
                    </li>

                </ul>

                <p>Присоединяйтесь к EasyHelp.kz и станьте частью команды профессионалов, готовых сделать дома наших
                    клиентов лучше. Мы верим в ваш потенциал и готовы помочь достичь новых высот в профессиональной карьере.
                </p>

                <NuxtLink to="/register" class="reg">Регистрация</NuxtLink>
            </div>

            <div class="right">
                <img src="@/assets/img/stage2.png" class="img-fluid" alt="">
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
    title: 'Для Исполнителя | EasyHelp',
    ogTitle: 'Для Исполнителя | EasyHelp',
    description: 'Для Исполнителя | EasyHelp',
    ogDescription: 'Для Исполнителя | EasyHelp',
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
                    color: #000;
                    text-decoration: none;

                    &:last-child {
                        color: var(--btn);
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