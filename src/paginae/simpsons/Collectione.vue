<script setup lang="ts">
import { Card, CardContent } from '@/components/ui/card' 
import { ref } from 'vue';
import { characters, type Character } from './data';

const listaSimpsons = ref<Character[]>(characters.slice(0,6))
</script>

<template>
    <div class="flex flex-col items-center justify-center gap-8 w-full max-w-350 my-8">
        <div class="text-center">
            <h1 class="font-bold text-xl lg:text-5xl mb-5">
                The Simpson Quote App
            </h1>
            <p class="mb-4">Click on the quote of your favorite character</p>
        </div>
        <div class="grid grid-cols-2 md:grid-cols-3 gap-8 mx-auto">
            <Card 
                class="cursor-pointer w-55 h-60 hover:bg-[#ee3133] hover:text-white transition-colors"
                v-for="character in listaSimpsons"
            >
                <CardContent class="flex flex-col items-center gap-1 w-full px-0">
                    <img 
                        :src="`/imagines/simpsons/${character.imago}`" alt=""
                        class="w-48 h-42 object-cover object-top mt-2 bg-[#ffde00] rounded-t-md border border-black"
                    >
                    <h2 class="font-medium text-lg">{{ character.nomen }}</h2>
                </CardContent>
            </Card>
        </div>
        

       
    </div>
</template>



<style scoped>

</style>