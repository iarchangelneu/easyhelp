<template>
    <div class="catalog">
        <h1>Каталог исполнителей</h1>

        <div class="filters">
            <div class="buttons">
                <button @click="filter = !filter" :class="{ activeFil: filter }">
                    <span>Фильтр</span>
                    <img src="@/assets/img/filter.svg" alt="" :class="{ activeImg: filter }">
                </button>
                <button @click="sort = !sort" :class="{ activeFil: sort }">
                    <span>Сортировать</span>
                    <img src="@/assets/img/filter.svg" alt="" :class="{ activeImg: sort }">
                </button>

                <div class="sort__body" :class="{ activeFilt: sort }">
                    <h3 @click="activeSort = 3, sortBy('-user__date_joined')" :class="{ activeSpan: activeSort == 3 }">Самые
                        новые</h3>
                    <h3 @click="activeSort = 4, sortBy('user__date_joined')" :class="{ activeSpan: activeSort == 4 }">Самые
                        старые</h3>
                    <h3 @click="activeSort = 5, sortBy('-rating')" :class="{ activeSpan: activeSort == 5 }">Самые
                        популярные</h3>
                </div>

                <div class="filter__body" :class="{ activeFilt: filter }">
                    <div>
                        <h1>Услуга</h1>
                        <div class="filters__box">
                            <div>
                                <label class="custom-checkbox" v-for="(category, index) in categories1" :key="index">
                                    <input type="checkbox" :value="index + 1" v-model="selectedCategories"
                                        @change="applyFilters">
                                    <p class="checkbox-text m-0">{{ category }}</p>
                                </label>
                            </div>
                            <div>
                                <label class="custom-checkbox" v-for="(category, index) in categories2" :key="index">
                                    <input type="checkbox" :value="index + 6" v-model="selectedCategories"
                                        @change="applyFilters">
                                    <p class="checkbox-text m-0">{{ category }}</p>
                                </label>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="catalog">
            <div class="catalog__item" v-for="item in catalog.results" :key="item.id">
                <img :src="item.photo" alt="">
                <h1>{{ item.user.first_name }}</h1>

                <ul v-if="item.features">
                    <li v-for="(feature, index) in item.features.split('\r\n')" :key="index">{{ feature }}
                    </li>
                </ul>

                <div class="price">
                    <NuxtLink class="w-100 text-center" :to="'/expert/' + item.id">Подробнее</NuxtLink>
                </div>
            </div>
        </div>

        <div class="text-right">
            <button @click="loadMoreProducts" ref="showmore">Посмотреть все</button>
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
            search: '',
            sort: false,
            filter: false,
            activeSort: 0,
            catalog: [],
            selectedCategories: [],
            minPrice: null,
            search: '',
            maxPrice: null,
            pathUrl: 'https://easyhelp.kz',
            categories1: ['Клининг', 'Ремонт дома', 'Сантехника', 'Строительство', 'Электрика'],
            categories2: ['Сборка мебели', 'Установка', 'Погрузка'],
        }
    },
    methods: {
        getCatalog() {
            const queryParams = new URLSearchParams(window.location.search);
            const categoryParam = queryParams.get('category');

            let url = `${this.pathUrl}/api/seller/all-seller`;
            if (categoryParam) {
                url += `?category__in=${categoryParam}`;
            }

            axios
                .get(url)
                .then(response => {
                    this.catalog = response.data;
                })
                .catch(error => {
                    console.error(error);
                });
        },
        loadMoreProducts() {
            if (this.catalog.next) {
                this.$refs.showmore.innerHTML = 'Загружаем'
                axios
                    .get(this.catalog.next)
                    .then(response => {
                        this.$refs.showmore.innerHTML = 'Показать еще'
                        this.catalog.results.push(...response.data.results);
                        this.catalog.next = response.data.next;
                    })
                    .catch(error => {
                        console.error(error);
                    });
            }
            else {
                this.$refs.showmore.innerHTML = 'Больше ничего нет (;'
            }
        },
        sortBy(ordering) {
            this.sort = false
            const path = `${this.pathUrl}/api/seller/all-seller?ordering=${ordering}`;
            axios
                .get(path)
                .then(response => {
                    this.catalog = response.data;

                })
                .catch(error => {
                    console.error(error);
                });
        },
        applyFilters() {
            const params = new URLSearchParams();
            if (this.minPrice !== null) {
                params.append('price__gte', this.minPrice);
            }
            if (this.maxPrice !== null) {
                params.append('price__lte', this.maxPrice);
            }

            if (this.selectedCategories.length > 0) {
                params.append('category', this.selectedCategories.join(','));
            }
            if (this.search) {
                params.append('name__icontains', this.search);
            }

            this.fetchFilteredProducts(params);
        },
        fetchFilteredProducts(params) {
            const path = `${this.pathUrl}/api/seller/all-seller?${params.toString()}`;
            axios
                .get(path)
                .then(response => {
                    this.catalog = response.data;
                })
                .catch(error => {
                    console.error(error);
                });
        },
        searchProducts() {
            const query = this.search.trim();
            if (query) {
                const queryParams = `?name__icontains=${query}`;
                this.fetchSearchResults(queryParams);
            } else {
                this.getCatalog();
            }
        },
        fetchSearchResults(queryParams) {
            const path = `${this.pathUrl}/api/products/all-product${queryParams}`;
            axios
                .get(path)
                .then(response => {
                    this.catalog = response.data;
                })
                .catch(error => {
                    console.error(error);
                });
        },
    },
    mounted() {
        this.getCatalog()
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
        position: relative;
        gap: 30px;

        .activeFilt {
            transform: scaleY(1) !important;
        }

        .sort__body {
            padding: 20px;
            text-align: center;
            position: absolute;
            left: 0;
            top: 120%;
            transition: all .3s ease;
            background: #fff;
            border: 1px solid #E3E3E3;
            box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
            transform: scaley(0);
            display: flex;
            flex-direction: column;
            gap: 14px;

            .activeSpan {
                color: #fff !important;
                background: #8BBAFF !important;
            }

            h3 {
                font-size: 20px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                font-family: var(--ral);
                color: #000;
                margin: 0;
                padding: 11px 15px;
                transition: all .3s ease;
                cursor: pointer;
            }

        }

        .filter__body {
            position: absolute;
            display: flex;
            gap: 70px;
            left: 0;
            top: 120%;
            transition: all .3s ease;

            transform: scaley(0);

            background: #fff;
            padding: 20px;

            border: 1px solid #E3E3E3;
            box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);

            .inputs {
                display: flex;
                gap: 5px;

                input {
                    border: 2px solid #000;
                    border-radius: 0;
                    padding: 6px 10px;
                    max-width: 140px;

                    font-size: 24px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--ral);
                    color: #000;

                    &::placeholder {
                        color: #000;
                    }
                }
            }

            .filters__box {
                display: flex;
                gap: 40px;

                div {
                    display: flex;
                    flex-direction: column;
                }
            }

            h1 {
                font-size: 20px;
                font-style: normal;
                font-weight: 700;
                line-height: normal;
                font-family: var(--ral);
                margin: 0 0 20px;
            }
        }

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

// .custom-checkbox p {
//     font-family: var(--ral);
//     font-size: 16px;
//     font-style: normal;
//     font-weight: 400;
//     line-height: 130%;
//     color: #000;
//     white-space: nowrap;
//     text-transform: uppercase;
// }

.custom-checkbox input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    border-radius: 3px;
}

.custom-checkbox .checkbox-text:before {
    content: '';
    display: inline-block;
    vertical-align: middle;
    width: 20px;
    height: 20px;
    margin-right: 10px;
    border: 2px solid #000;
    border-radius: 3px;
    margin-bottom: 3px;
}

.custom-checkbox input[type="checkbox"]:checked+.checkbox-text:before {
    content: url('@/assets/img/check.svg');
    font-size: 16px;
    color: black;
    text-align: center;
    line-height: 20px;
    background: transparent;
}

.custom-checkbox {
    margin-bottom: 15px;

}

.custom-checkbox:last-child {
    margin-bottom: 0 !important;

    @media (max-width: 1024px) {
        margin-bottom: 22px !important;
    }
}
</style>