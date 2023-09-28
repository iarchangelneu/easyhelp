<template>
    <footer v-if="!hideFooterOnPages.includes($route.name)">
        <div class="footer__body">
            <NuxtLink to="/">
                <h1>
                    EasyHelp.kz
                </h1>
            </NuxtLink>
            <div class="links">
                <div>
                    <NuxtLink to="/catalog">Каталог услуг</NuxtLink>
                    <NuxtLink to="/experts">Каталог исполнителей</NuxtLink>
                </div>
                <div>
                    <NuxtLink to="/for-seller">Для заказчика</NuxtLink>
                    <NuxtLink to="/for-buyer">Для исполнителя</NuxtLink>
                </div>
                <div>
                    <NuxtLink to="/polytics">Политика конфиденциальности</NuxtLink>
                    <NuxtLink to="/terms">Пользовательское соглашение</NuxtLink>
                </div>
            </div>
        </div>

        <div class="text-center">
            <small>2023 © EasyHelp.kz </small>
        </div>
    </footer>
</template>
<script>
export default {
    data() {
        return {
            hideFooterOnPages: ['login', 'register'],
        }
    }
}
</script>
<style lang="scss" scoped>
footer {
    background: var(--btn);
    padding: 90px 0 50px 210px;

    @media (max-width: 1600px) {
        padding: 90px 0 50px 140px;
    }

    @media (max-width: 1400px) {
        padding: 50px 0 50px 50px;
    }

    @media (max-width: 1024px) {
        padding: 30px 20px 55px;
    }

    .text-center {
        @media (max-width: 1024px) {
            text-align: left !important;
        }
    }

    small {
        font-size: 16px;
        font-style: normal;
        font-weight: 500;
        line-height: 130%;
        font-family: var(--ral);
        color: #fff;
        margin-top: 50px;
        display: block;

        @media (max-width: 1024px) {
            margin-top: 28px;
        }
    }

    a {
        text-decoration: none;
    }

    .footer__body {
        display: flex;
        align-items: center;
        gap: 131px;

        @media (max-width: 1400px) {
            gap: 50px;
        }

        @media (max-width: 1024px) {
            flex-direction: column;
            gap: 25px;
            align-items: flex-start;
        }
    }

    .links {
        display: flex;
        gap: 50px;

        @media (max-width: 1024px) {
            gap: 25px;
            flex-direction: column;
        }

        div {
            display: flex;
            flex-direction: column;
            gap: 25px;

            a {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: normal;
                font-family: var(--ral);
                color: #fff;

                @media (max-width: 1400px) {
                    font-size: 16px;
                }

                @media (max-width: 1024px) {
                    font-size: 20px;
                }
            }
        }

    }

    h1 {
        font-size: 40px;
        font-style: normal;
        font-weight: 600;
        line-height: normal;
        font-family: var(--ral);
        color: #fff;
        margin: 0;
    }
}
</style>