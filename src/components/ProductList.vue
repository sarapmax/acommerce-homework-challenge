<template>
    <div class="container mx-auto py-10 px-4">
        <p class="text-lg">Item 1 to {{ products.length}} of {{ products.length }}</p>
        <div class="flex flex-wrap grid gap-4 grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 mt-4">
            <div v-for="product in products" :key="product.id" class="shadow p-4 hover:shadow-lg cursor-pointer">
                <img :src="product.image_url" :alt="product.title">
                <div>
                    <h3 class="font-normal text-lg mt-2">{{ product.title }}</h3>
                    <p class="mt-1">{{ product.created_at | diffForHumans }}</p>
                    <div class="flex mt-2" v-show="product.vote > 0">
                        <svg v-for="(star, key) in product.vote" :key="key" class="mr-2"
                             xmlns="http://www.w3.org/2000/svg"
                             viewBox="0 0 24 24"
                             width="24" height="24">
                            <path fill="none" d="M0 0h24v24H0z"/>
                            <path d="M12 18.26l-7.053 3.948 1.575-7.928L.587 8.792l8.027-.952L12 .5l3.386 7.34 8.027.952-5.935 5.488 1.575 7.928z"
                                  fill="rgba(233,52,38,1)"/>
                        </svg>
                    </div>
                    <p class="mt-4 font-semibold">{{ product.price | toBaht }}</p>
                </div>
            </div>
        </div>
        <div class="mt-6">
            <ul class="flex justify-center">
                <li class="h-10 w-10 flex items-center justify-center bg-red-300 hover:bg-red-600 cursor-pointer mx-1">
                    1
                </li>
                <li class="h-10 w-10 flex items-center justify-center bg-red-300 hover:bg-red-600 cursor-pointer mx-1">
                    2
                </li>
                <li class="h-10 w-10 flex items-center justify-center bg-gray-300 hover:bg-gray-500 cursor-pointer mx-1">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="32" height="32">
                        <path fill="none" d="M0 0h24v24H0z"/>
                        <path d="M13.172 12l-4.95-4.95 1.414-1.414L16 12l-6.364 6.364-1.414-1.414z"
                              fill="rgba(255,255,255,1)"/>
                    </svg>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    import moment from 'moment'
    import list from './json/list.json'

    export default {
        name: 'HelloWorld',
        data() {
            return {
                products: list
            }
        },

        filters: {
            // eslint-disable-next-line no-unused-vars
            diffForHumans(value) {
                return moment("2019-01-01", "YYYY-MM-DD H:mm:ss").fromNow()
            },

            toBaht(value) {
                return '฿' + value.toFixed(2).replace(/\d(?=(\d{3})+\.)/g, '$&,')
            }
        }
    }
</script>
