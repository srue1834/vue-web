<script setup lang="ts">
import { computed, ref, watch } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import { characters, type Character } from './data';
import { CheckIcon, ChevronsUpDownIcon } from 'lucide-vue-next'
import { cn } from '@/lib/utils'
import { Button } from '@/components/ui/button'
import {
  Command,
  CommandEmpty,
  CommandGroup,
  CommandInput,
  CommandItem,
  CommandList,
} from '@/components/ui/command'
import {
  Popover,
  PopoverContent,
  PopoverTrigger,
} from '@/components/ui/popover'

const route = useRoute()
const router = useRouter()

const character = ref<Character | undefined>(
    characters.find(char => char.id === Number(route.params.id))
)

const simpsons = characters.map(char => ({
    value: char.id.toString(),
    label: char.nomen
}))

const open = ref(false)
const value = ref(route.params.id?.toString() || "")

watch(() => route.params.id, (newId) => {
    character.value = characters.find(char => char.id === Number(newId))
    value.value = newId?.toString() || ''
})

const selectCharacter = (characterId: string) => {
  value.value = characterId
  open.value = false
  router.push(`/simpsons/gallery/${characterId}`)
}

const selectedLabel = computed(() => {
    if(!value.value) return 'Selecciona un personaje ...'
    return simpsons.find(simpson => simpson.value === value.value )?.label || 'Selecciona un personaje ...'
})

</script>

<template>
    <div
        v-if="character"
        class="w-full max-w-350 md:mx-auto my-8 px-5 md:px-20"
    >
        <div class="mb-8">
            <label class="block text-lg font-semibold mb-2 text-gray-800">Buscar personaje:</label>
            <Popover v-model:open="open">
                <PopoverTrigger as-child>
                    <Button
                        variant="outline"
                        role="combobox"
                        :aria-expanded="open"
                        class="w-50 justify-between bg-[rgb(239,68,68)] hover:bg-[#ffde00] border-2 border-black font-semibold text-white shadow-md"
                    >
                        {{ selectedLabel }}
                        <ChevronsUpDownIcon class="ml-2 h-4 w-4 shrink-0 opacity-50" />
                    </Button>
                </PopoverTrigger>
                <PopoverContent class="w-50 p-0 border-2 border-black bg-white">
                    <Command>
                        <CommandInput class="border-b-2 border-gray-200" placeholder="Buscar ..." />
                        <CommandList>
                            <CommandEmpty>No se encontró</CommandEmpty>
                            <CommandGroup>
                                <CommandItem
                                    v-for="simpson in simpsons"
                                    :key="simpson.value"
                                    :value="simpson.value"
                                    @select="selectCharacter(simpson.value)"
                                    class="hover:bg-black hover:text-white cursor-pointer font-medium transition-colors"
                                >
                                    {{ simpson.label }}
                                <CheckIcon
                                    :class="cn(
                                    'ml-auto',
                                    value === simpson.value ? 'opacity-100' : 'opacity-0',
                                    )"
                                />
                                </CommandItem>
                            </CommandGroup>
                        </CommandList>
                    </Command>
                </PopoverContent>
            </Popover>

        </div>
        
        <div class="flex flex-col lg:flex-row lg:justify-between md:items-center gap-8">
            <div>
                <h1 class="mb-5 text-3xl font-bold leading-9 lg:text-5xl lg:leading-none"> 
                    {{ character.nomen }}
                </h1>

                <div class="lg:max-w-3xl">
                    <p class="mb-10 max-w-3xl text-xl font-light leading-7 lg:text-2xl lg:leading-8">
                        {{ character.descriptione }}
                    </p>
                            
                    <div 
                        class="flex max-w-3xl cursor-pointer items-center justify-center rounded-lg border border-black bg-red-500 p-5"
                        @click="router.push('/simpsons/gallery')"
                    >
                        <p class="mb-5 text-center text-[1.8rem] font-extralight leading-[2.2rem] text-white lg:text-[2.2rem] lg:leading-10"> 
                            « {{ character.quote }} »
                        </p>
                    </div>
                </div>
            </div>
        

            <figure class="flex min-w-min justify-center">
                <img
                    class="object-contain"
                    :src="`/imagines/simpsons/${character.imago}`" alt="" 
                />
            </figure>
        </div>
    </div>
    
</template>

<style scoped></style>