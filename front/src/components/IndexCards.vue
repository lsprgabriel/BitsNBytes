<template>
    <span>
        <div class="flex overflow-hidden whitespace-nowrap no-scrollbar relative scroll-smooth snap-x" id="container">
            <div v-for="card in cards.data" :key="card.index">
                <div class="flex px-3 m-2 snap-center">
                    <div class="rounded-lg shadow-md bg-[#15393C] w-[300px] lg:w-[410px]">
                        <a href="/">
                            <!-- colocar imagens no banco amanhã -->
                            <img class="rounded-t-lg h-80 w-full" :src="card.photo" />
                        </a>
                        <div class="p-6">
                            <div class="flex justify-between">
                                <h5 class="text-white text-xl font-medium mb-2">
                                    {{ card.name }}
                                </h5>
                                <h5 class="text-white text-xl font-medium mb-2">{{ card.age }} {{ age(card.age) }}</h5>
                            </div>

                            <p class="text-white text-base mb-4 h-20">
                                {{ card.description }}
                            </p>
                            <div class="flex justify-center flex-row">
                                <router-link
                                    v-bind:to="'/comentar/' + card.id"
                                    type="button"
                                    class="inline-block px-6 py-2.5 mr-3 bg-white text-[#15393C] cursor-pointer font-semibold text-xs leading-tight uppercase rounded shadow-md"
                                    >Comentar</router-link
                                >
                                <router-link
                                    v-bind:to="'/galeria/' + card.id"
                                    type="button"
                                    class="inline-block px-6 py-2.5 ml-3 bg-white text-[#15393C] cursor-pointer font-semibold text-xs leading-tight uppercase rounded shadow-md"
                                    >Galeria</router-link
                                >
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <span v-if="showControls">
            <button class="card-control left" @click="left"><ChevronLeftIcon class="card-control w-20" /></button>
            <button class="card-control right" @click="right"><ChevronRightIcon class="card-control w-20" /></button>
        </span>
    </span>
</template>

<script>
import axios from "axios";
import {ChevronLeftIcon} from "@heroicons/vue/solid";
import {ChevronRightIcon} from "@heroicons/vue/solid";

export default {
    name: "App",
    data() {
        return {
            cards: [],
            showControls: true,
        };
    },
    mounted() {
        axios.get("https://if-acolhe-back.herokuapp.com/api/dogs").then((response) => (this.cards = response));
    },
    methods: {
        left() {
            document.getElementById("container").scrollLeft -= 320;
        },
        right() {
            document.getElementById("container").scrollLeft += 320;
        },

        age(age) {
            if (age > 1) {
                return "Anos";
            } else {
                return "Ano";
            }
        },
    },
    components: {
        ChevronLeftIcon,
        ChevronRightIcon,
    },
};
</script>

<style scoped>
.card-control {
    background-color: transparent;
    border: none;
    position: absolute;
    width: 70px;
    top: calc(50% - 25px);
    color: #15393c81;

    transition: 0.5s;
}
.card-control:hover {
    color: #15393c;
}
.left {
    left: 0;
}
.right {
    right: 0;
}
</style>
