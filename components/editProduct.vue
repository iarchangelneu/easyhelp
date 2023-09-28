<template>
    <div>
        <div class="course">
            <div class="course__left">
                <div>
                    <label for="name">Название услуги</label>
                    <input type="text" id="name" name="name" placeholder="Введите название" ref="name" v-model="name">
                </div>
                <div class="select">
                    <div class="mb-0">
                        <label for="select">Выберите категорию</label>
                        <select name="select" id="select" v-model="selectedCategory" ref="select">
                            <option v-for="(category, index) in categories" :key="index" :value="category.id">{{
                                category.name
                            }}</option>
                        </select>
                    </div>
                    <span v-if="selectedCategory !== null">
                        {{ getCategoryName(selectedCategory) }}
                        <img src="@/assets/img/del.svg" alt="" loading="lazy" @click="clearSelection">
                    </span>
                </div>

                <div class="discount">
                    <div>
                        <label for="name">Введите цену</label>
                        <input type="number" id="name" name="name" placeholder="Цена за товар" v-model="price">
                    </div>

                </div>
                <div>
                    <label for="name">Загрузка изображения</label>
                    <div class="mb-0 fileupload" @dragover.prevent="highlightDropArea"
                        @dragleave.prevent="unhighlightDropArea" @drop.prevent="handleDrop" @click="openFileInput">
                        <span>{{ alert }}</span>
                        <small>Открыть</small>
                        <input type="file" ref="fileInput" style="display: none" accept="image/*" multiple
                            @change="handleFileInput" />
                    </div>


                    <div class="uploaded-images">
                        <div v-for="(image, index) in uploadedImages" :key="index" class="uploaded-image">
                            <img :src="image.url" alt="Uploaded Image" />
                        </div>
                    </div>
                </div>
            </div>

            <div class="course__right">
                <div>
                    <label for="tabs">Особенности услуги (До 4)</label>
                    <div class="custom-textarea">
                        <textarea class="features-list" сols="30" rows="4" ref="featuresList" v-model="courseFeaturesText"
                            @keydown="handleKeyDown"></textarea>
                    </div>
                </div>
                <div>
                    <label for="tabs">Описание услуги</label>
                    <ClientOnly>
                        <QuillEditor theme="bubble" toolbar="full" v-model:content="description" contentType="html" />
                    </ClientOnly>
                </div>
            </div>
        </div>

        <div class="text-center">
            <button ref="createProduct" @click="submitForm">Опубликовать товар</button>
        </div>

    </div>
</template>
<script>
import axios from 'axios';
import global from '~/mixins/global';
export default {
    mixins: [global],
    props: {
        productId: Number,
    },
    data() {
        return {
            pathUrl: 'https://EasyHelp.kz',
            selectedCategory: null,
            discount: 0,
            price: 0,
            name: '',
            shortDesc: '',
            description: '',
            alert: 'Перетащите файлы сюда или откройте вручную',
            uploadedImages: [],
            courseFeaturesText: '',
            product: [],
            categories: [
                { id: 1, name: "Стикеры" },
                { id: 2, name: "Одежда" },
                { id: 3, name: "Чехлы на телефон" },
                { id: 4, name: "Постеры" },
                { id: 5, name: "Для дома" },
                { id: 6, name: "Аксессуары" },
                { id: 7, name: "Для питомцев" },
                { id: 8, name: "Канцелярия" },
                { id: 9, name: "Для детей" },
                { id: 10, name: "Подарочные наборы" },
            ],
        }
    },

    methods: {
        async submitForm() {
            this.$refs.save.innerHTML = 'Сохраняем'
            const path = `${this.pathUrl}/api/seller/seller-lk/edit-product/${this.productId}`
            const csrf = this.getCSRFToken()
            const formData = new FormData();

            const filesToUpload = this.uploadedImages
                .filter(item => item.file instanceof File)
                .map(item => item.file);


            formData.append('name', this.name);
            formData.append('category', this.selectedCategory);
            formData.append('price', this.price);
            formData.append('discount', this.discount);
            filesToUpload.forEach(file => {
                formData.append('add_image', file);
            });
            formData.append('description', this.description);
            formData.append('short_description', this.shortDesc);
            formData.append('key_features', this.courseFeaturesText);
            formData.append('show', true);



            try {
                axios.defaults.headers.common['X-CSRFToken'] = csrf;
                const response = await axios.put(path, formData);

                console.log('Форма успешно отправлена', response);
                if (response.status == 200) {
                    this.$refs.save.innerHTML = 'Товар успешно сохранен'
                }
            } catch (error) {
                console.error('Ошибка при отправке формы', error);

                if (error.message) {
                    this.$refs.save.innerHTML = error.message
                }

            }
        },
        getProduct() {
            const path = `${this.pathUrl}/api/seller/seller-lk/edit-product/${this.productId}`
            axios
                .get(path)
                .then(response => {
                    this.product = response.data
                    this.courseFeaturesText = response.data.key_features
                    this.description = response.data.description
                    this.name = response.data.name
                    this.discount = response.data.discount
                    this.price = response.data.price
                    this.shortDesc = response.data.short_description
                    this.selectedCategory = response.data.category
                })
                .catch(error => {
                    console.error(error)
                })
        },
        handleKeyDown(event) {
            if (event.key === 'Backspace' && !this.courseFeaturesText) {
                event.preventDefault();

            }

            const lines = this.courseFeaturesText.split('\n');
            if (lines.length >= 4 && event.key === 'Enter') {
                event.preventDefault();
                this.$refs.featuresList.style.borderColor = 'red'
                return;
            }
        },
        getCategoryName(categoryId) {
            const category = this.categories.find((c) => c.id === categoryId);
            return category ? category.name : "";
        },
        clearSelection() {
            this.selectedCategory = null;
        },
        limitValue() {
            if (this.discount > 100) {
                this.discount = 100;
            }
        },
        highlightDropArea(event) {
            event.currentTarget.classList.add('highlight');
        },
        unhighlightDropArea(event) {
            event.currentTarget.classList.remove('highlight');
        },
        handleDrop(event) {
            event.preventDefault();
            this.unhighlightDropArea(event);

            const files = event.dataTransfer.files;
            this.processFiles(files);
        },
        handleFileInput() {
            const files = this.$refs.fileInput.files;
            this.processFiles(files);
        },
        processFiles(files) {
            const imageFiles = [];
            for (let i = 0; i < files.length; i++) {
                if (files[i].type.startsWith('image/')) {
                    imageFiles.push(files[i]);
                }
            }

            if (this.uploadedImages.length + imageFiles.length > 1) {
                this.alert = 'Можно загрузить не более 1 изображениz'
                return;
            }

            imageFiles.forEach((file) => {
                const imageUrl = URL.createObjectURL(file);
                this.uploadedImages.push({ url: imageUrl, file });
            });

        },
        openFileInput() {

            this.$refs.fileInput.click();
        },
    },
    mounted() {
        this.getProduct()
    },
}
</script>
<script setup>
import { QuillEditor } from '@vueup/vue-quill';
import '@vueup/vue-quill/dist/vue-quill.snow.css';
import '@vueup/vue-quill/dist/vue-quill.bubble.css';
useSeoMeta({
    title: 'Редактирование Товара | EasyHelp',
    ogTitle: 'Редактирование Товара | EasyHelp',
    description: 'Редактирование Товара | EasyHelp',
    ogDescription: 'Редактирование Товара | EasyHelp',
})
</script>
<style lang="scss" scoped>
.text-center {
    button {
        margin-top: 30px;
        padding: 10px 20px;
        border: 2px solid var(--btn);
        border-radius: 20px;
        background: transparent;

        font-size: 16px;
        font-style: normal;
        font-weight: 500;
        line-height: 130%;
        font-family: var(--ral);
        color: var(--btn);
        text-transform: uppercase;

        transition: all .3s ease;

        &:hover {
            color: #fff;
            background: var(--btn);
        }
    }
}

.course {
    margin-top: 34px;
    display: flex;
    gap: 20px;
    width: 100%;

    @media (max-width: 1024px) {
        flex-direction: column;
        margin-top: 20px;
    }

    label,
    input {
        display: block;
    }

    label {
        margin-left: 10px;
        font-size: 16px;
        font-style: normal;
        font-weight: 500;
        line-height: 110%;
        font-family: var(--ral);
        color: #000;
    }

    .uploaded-images {
        display: flex;
        flex-wrap: wrap;
        gap: 9px;
        margin-top: 20px;

        .uploaded-image {
            max-width: auto !important;
            width: auto !important;
        }

        img {
            width: 259px;
            height: 177px;

            @media (max-width: 1024px) {
                width: 165px;
                height: 110px;
            }
        }
    }

    textarea {
        background: #F6FAFF;
    }

    input,
    select {
        background: #F6FAFF;
        border: 1px solid #E3E3E3;
        border-radius: 0;
        padding: 10px;
        width: 100%;

        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: 130%;
        font-family: var(--ral);
        color: #000;
    }

    .course__left {
        max-width: 527px;

        @media (max-width: 1024px) {
            max-width: 100%;
            width: 100%;
        }

        .highlight {
            border: 2px dashed green !important;
            cursor: pointer;
            /* Добавьте курсор-указатель, чтобы показать, что область можно нажать */
        }

        .fileupload {
            border-radius: 0;
            border: 1px solid #E3E3E3;
            padding: 10px;
            display: flex;
            justify-content: space-between;
            cursor: pointer;
            background: #F6FAFF;


            span {
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--ral);
                color: #3C3C3C;
            }

            small {
                font-size: 16px;
                font-style: normal;
                font-weight: 500;
                line-height: 130%;
                text-decoration-line: underline;
                font-family: var(--ral);
                color: #000;
            }
        }

        width: 100%;

        div {
            margin-bottom: 20px;
            max-width: 527px;

            @media (max-width: 1024px) {
                max-width: 100%;
                width: 100%;
            }

            &:last-child {
                margin-bottom: 0;
            }
        }

        .discount {
            display: flex;
            gap: 10px;

            div {
                flex: 1;
            }
        }

        .select {
            display: flex;
            align-items: flex-end;
            flex-wrap: wrap;
            gap: 10px;

            @media (max-width: 1024px) {
                flex-direction: column;
                align-items: flex-start;
            }

            span {
                flex: 1;
                padding: 11px 10px;
                margin-top: 4px;
                border: 1px solid #E3E3E3;
                border-radius: 0;

                display: flex;
                align-items: flex-start;
                justify-content: space-between;
                gap: 10px;
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--ral);
                color: #000;

                @media (max-width: 1024px) {}

                img {
                    cursor: pointer;
                }
            }
        }
    }

    .course__right {
        width: 100%;

        .custom-textarea {
            width: 100%;
            background: transparent;

        }

        .features-list {
            outline: none;
            white-space: pre-wrap;
            background: #F6FAFF;
            width: 100%;
        }

        textarea {
            width: 100%;
            border-radius: 0;
            border: 1px solid #E3E3E3;
            background: transparent;
            padding: 20px;
        }

        div {
            margin-bottom: 20px;

            &:last-child {
                margin-bottom: 0;
            }
        }
    }
}
</style>