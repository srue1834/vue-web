<script setup lang="ts">
import { Card, CardContent } from '@/components/ui/card'
import {
  Pagination,
  PaginationContent,
  PaginationItem,
  PaginationNext,
  PaginationPrevious,
} from '@/components/ui/pagination'

import { computed, ref } from 'vue'
import { characters } from './data'
import { useRouter } from 'vue-router'

const router = useRouter()

const inPagina = 6
const nuncPagina = ref(1)

const totalPaginae = Math.ceil(characters.length / inPagina)

const listaSimpsons = computed(() => {
  const inicio = (nuncPagina.value - 1) * inPagina
  const fin = inicio + inPagina
  return characters.slice(inicio, fin)
})

const ireAdPaginam = (pagina: number) => {
  if (pagina >= 1 && pagina <= totalPaginae) {
    nuncPagina.value = pagina
  }
}
</script>

<template>
  <div class="flex flex-col items-center justify-center gap-8 w-full max-w-350 my-8 mx-auto">
    
    <!-- Header -->
    <div class="text-center">
      <h1 class="font-bold text-xl lg:text-5xl mb-5">
        The Simpson Quote App
      </h1>
      <p class="mb-4">
        Click on the quote of your favorite character
      </p>
    </div>

    <!-- Cards -->
    <div class="grid grid-cols-2 md:grid-cols-3 gap-8 mx-auto">
      <Card
        v-for="character in listaSimpsons"
        :key="character.id"
        class="cursor-pointer w-55 h-60 hover:bg-[#ee3133] hover:text-white transition-colors"
      >
        <CardContent
          class="flex flex-col items-center gap-1 w-full px-0"
          @click="router.push(`/simpsons/gallery/${character.id}`)"
        >
          <img
            :src="`/imagines/simpsons/${character.imago}`"
            alt=""
            class="w-48 h-42 object-cover object-top mt-2 bg-[#ffde00] rounded-t-md border border-black"
          />

          <h2 class="font-medium text-lg">
            {{ character.nomen }}
          </h2>
        </CardContent>
      </Card>
    </div>

    <Pagination
      v-slot="{ page }"
      :items-per-page="inPagina"
      :total="characters.length"
      :default-page="nuncPagina"
      @update:page="ireAdPaginam"
    >
      <PaginationContent
        v-slot="{ items }"
        class="flex items-center justify-center gap-2 mt-4"
      >
        <PaginationPrevious
          @click="ireAdPaginam(nuncPagina - 1)"
          class="px-4 py-2 rounded-md font-medium transition-colors"
          :class="
            nuncPagina === 1
              ? 'bg-gray-200 text-gray-400 pointer-events-none'
              : 'bg-[#ffde00] hover:bg-[#ee3133] hover:text-white'
          "
        />

        <template v-for="(item, index) in items" :key="index">
          <PaginationItem
            v-if="item.type === 'page'"
            :value="item.value"
            :is-active="item.value === page"
            class="w-10 h-10 rounded-md font-medium transition-colors flex items-center justify-center"
            :class="
              nuncPagina === item.value
                ? 'bg-[#ee3133] text-white'
                : 'bg-[#ffde00] hover:bg-[#ee3133] hover:text-white'
            "
            @click="ireAdPaginam(item.value)"
          >
            {{ item.value }}
          </PaginationItem>
        </template>

        <PaginationNext
          @click="ireAdPaginam(nuncPagina + 1)"
          class="px-4 py-2 rounded-md font-medium transition-colors"
          :class="
            nuncPagina === totalPaginae
              ? 'bg-gray-200 text-gray-400 pointer-events-none'
              : 'bg-[#ffde00] hover:bg-[#ee3133] hover:text-white'
          "
        />
      </PaginationContent>
    </Pagination>

  </div>
</template>