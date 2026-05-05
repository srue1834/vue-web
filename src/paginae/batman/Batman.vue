<script lang="ts" setup>

import { scrollToSection } from '@/utils/scrollToSection';
import { useMouseMotio } from '@/composables/useMouseMotio';
import CarrusImaginum from '@/components/CarrusImaginum.vue';
import NavigatorPrimarius from '@/components/NavigatorPrimarius.vue';
import { Label } from '@/components/ui/label'
import { Input } from '@/components/ui/input'
import { Button } from '@/components/ui/button'
import { Calendar } from '@/components/ui/calendar'
import { toast } from 'vue-sonner'


import {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from '@/components/ui/select'

import {
  Popover,
  PopoverContent,
  PopoverTrigger,
} from '@/components/ui/popover'

import type { DateValue } from 'reka-ui';
import { ref } from 'vue';
import { Loader2, Phone, MapPin, Mail, MessageCircle, X, Instagram, Linkedin, LucideBadgeCheck } from 'lucide-vue-next';

const photos = ["justice", "arkham", "superman", "varios", "villana", "villano", "grupo", "robin", "anne", "joker", "resplandor", "cat", "gafas", "league", "fondoVerde"]; 

const {mousePositione, cumMouseMove, cumMouseLeave } = useMouseMotio()

const menuItems = [
    {
        label: 'Portada',
        href: '#',
        onClick: () => scrollToSection('#')
    },
    {
        label: 'Vehículos',
        href: '#vehiculis',
        onClick: () => scrollToSection('#vehiculis')
    },
    {
        label: 'Imágenes',
        href: '#videre',
        onClick: () => scrollToSection('#videre')
    },
    {
        label: 'Contacto',
        href: '#contactus',
        onClick: () => scrollToSection('#contactus')
    }
]

const dies = ref<DateValue>()
const nomen = ref<string>('')
const cognomen = ref<string>('')
const missio = ref<string>('')

const estLoading = ref<boolean>(false)
    

const mittereSubmit = async() => {
    estLoading.value = true
    toast(`Solicitud enviada correctamente
    - Nombre: ${nomen.value} ${cognomen.value}
    - Misión: ${missio.value}
    Fecha: ${dies.value ? `${dies.value.day}/${dies.value.month}/${dies.value.year}`:'No especificada'}`, {
        duration: 4000,
        position: "top-right",
        icon: LucideBadgeCheck,
        style: {
            background: "#201C3B",
            color: "#fff",
            whiteSpace: "pre-wrap"
        }
    })
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    estLoading.value = false
    nomen.value = ''
    cognomen.value = ''
    missio.value = ''
    dies.value = undefined
    

}


</script>

<template>
    <div class="font-sans">
        <NavigatorPrimarius :items="menuItems" home-route="/" />
  
        <header class="relative">
            <h1 class="pointer-events-none absolute top-[50vw] w-full text-center text-7xl text-white font-[batman]">
                Batman
            </h1>
    
            <div
                id="titulus-batman"
                class="aspect-8/7 bg-[url('/imagines/batman/batman.jpg')] bg-size-[100%_100%] bg-center transition-[background-size] duration-300 hover:bg-size-[115%_115%]"
                @mousemove="cumMouseMove"
                @mouseleave="cumMouseLeave"
                :style="{
                backgroundPositionX: `calc(50% + ${mousePositione.x}px)`,
                backgroundPositionY: `calc(50% + ${mousePositione.y}px)`,
                transition: 'background-position 0.1s ease-out, background-size 0.3s ease'
                }">
            </div>
    
            <p class="pointer-events-none absolute top-[25vw] hidden w-full text-center text-3xl text-white font-[batman] md:block">
                Él puede tomar la decisión que nadie más puede, la decisión correcta
            </p>
        </header>
  
        <section
            id="vehiculis"
            class="mx-auto flex max-w-127.5 flex-col py-16 sm:max-w-xl md:max-w-225 lg:max-w-7xl"
        >
            <div class="order-1 flex flex-col lg:flex-row">
                <div class="order-2 flex h-135 flex-col items-center justify-around bg-[rgba(220,220,220,0.2)] py-6 md:h-80 md:flex-row lg:h-140 lg:flex-col">
                    <div class="flex w-[90%] flex-col items-center md:w-[40%] lg:w-[90%]">
                        <h2 class="pb-4 text-[1.7rem] font-semibold text-black/70">Avión</h2>
                        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vehicula vulputate elit eget fermentum. Ut laoreet ante lacus. Quisque ut tincidunt metus.</p>
                        <small class="p-4 font-bold">Fabricado en 2005</small>
                    </div>
                    <img class="w-112.5 md:order-first lg:order-0" src="/imagines/batman/avion.jpg" />
                </div>
    
                <div class="flex h-135 flex-col items-center justify-around bg-[rgba(220,220,220,0.8)] py-6 md:h-80 md:flex-row lg:h-140 lg:flex-col">
                    <div class="flex w-[90%] flex-col items-center md:w-[40%] lg:w-[90%]">
                        <h2 class="pb-4 text-[1.7rem] font-semibold text-black/70">Moto</h2>
                        <p>Nulla aliquip cupidatat voluptate veniam nostrud aliquip sit enim officia. Sit eu pariatur officia qui dolor adipisicing cupidatat.</p>
                        <small class="p-4 font-bold">Fabricado en 2006</small>
                    </div>
                    <img class="w-112.5" src="/imagines/batman/moto.jpg" />
                </div>
    
                <div class="order-3 flex h-135 flex-col items-center justify-around bg-[rgba(220,220,220,0.8)] py-6 md:h-80 md:flex-row lg:h-140 lg:flex-col">
                    <div class="flex w-[90%] flex-col items-center md:w-[40%] lg:w-[90%]">
                        <h2 class="pb-4 text-[1.7rem] font-semibold text-black/70">Coche</h2>
                        <p>Irure adipisicing est minim eu ad dolor. Eu ea commodo pariatur ut occaecat in cupidatat reprehenderit ut laborum duis.</p>
                        <small class="p-4 font-bold">Fabricado en 2007</small>
                    </div>
                    <img class="w-112.5" src="/imagines/batman/car.jpg" />
                </div>
            </div>
    
            <div class="flex h-22 items-center justify-center bg-black/70 text-3xl text-white">
                <h1>Vehículos de Batman</h1>
            </div>
        </section>
  
        <section
            id="videre"
            class="flex min-h-[60vh] w-full items-center justify-center bg-gray-900 lg:min-h-[95vh]"
        >
            <CarrusImaginum
                base-path="/imagines/batman"
                :photos="photos"
                :autoplay-delay="3000"
            />
        </section>

        <section id="contactus" class="w-full py-12 bg-gray-100">

            <div class="container mx-auto max-w-5xl px-4">

                <h2 class="text-3xl font-bold text-gray-900 mb-8 text-center">Contacta con Batman</h2>
                    
                <div class="flex flex-col lg:flex-row gap-8 items-center">

                        <!-- Mapa de Google Maps -->
                    <div class="hidden lg:block w-full lg:w-1/2 rounded-lg overflow-hidden shadow-lg">
                        <div class="aspect-square">
                            <iframe 
                                src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3079.495076872935!2d-0.3410958!3d39.4807342!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0xd60487c5d604077%3A0x150fdf31fdc5a6f6!2sUniversitat%20Polit%C3%A8cnica%20de%20Val%C3%A8ncia%20(UPV)!5e0!3m2!1ses!2sgt!4v1777931767123!5m2!1ses!2sgt" 
                                width="600" 
                                height="450" 
                                :style="{border:0}"
                                allowfullscreen
                                loading="lazy" 
                                referrerpolicy="no-referrer-when-downgrade"
                            ></iframe>
                            
                        </div>
                    </div>

                        <!-- Formulario -->
                    <div class="w-full max-w-md mx-auto lg:max-w-none lg:w-1/2 ">

                        <form  
                            class="space-y-6 bg-white p-8 rounded-lg shadow-lg aspect-square"
                            @submit.prevent="mittereSubmit"
                        >
                            <div class="space-y-2">
                                    
                                <Label for="nomen">Nombre</Label>
                                <Input id="nomen" v-model="nomen" required/>

                            </div>
                                
                            <div class="space-y-2">
                                
                                <Label for="cognomen">Apellidos</Label>
                                <Input id="cognomen" v-model="cognomen" required/>

                            </div>

                            <div class="space-y-2">

                                <Select required v-model="missio">
                                    <SelectTrigger class="border-gray-200 bg-white text-gray-900">
                                        <SelectValue placeholder="Selecciona una misión" />
                                    </SelectTrigger>

                                    <SelectContent>
                                        <SelectGroup>
                                            <SelectItem value="rescatare">
                                                Rescate de rehenes
                                            </SelectItem>
                                            <SelectItem value="investigare">
                                                Investigación criminal
                                            </SelectItem>
                                            <SelectItem value="persequi">
                                                Persecución de villanos
                                            </SelectItem>
                                            <SelectItem value="defendere">
                                                Defensa de Gotham
                                            </SelectItem>
                                           
                                        </SelectGroup>
                                    </SelectContent>
                                </Select>

                            </div>

                            <div class="space-y-2">

                                <Label>Fecha de la misión</Label>
                                <Popover>
                                    <PopoverTrigger asChild>
                                        <Button variant="outline">
                                            <span v-if="dies">
                                                {{ dies.day }}/{{ dies.month }}/{{ dies.year }}
                                            </span>
                                            <span v-else class="text-gray-500">
                                                Selecciona una fecha
                                            </span>
                                        </Button>
                                    </PopoverTrigger>
                                    <PopoverContent class="w-80">
                                        <Calendar v-model="dies"/>
                                    </PopoverContent>
                                </Popover>
                            </div>
                                <Button
                                    type="submit"
                                    class="w-full bg-[rgb(106,90,205)] hover:bg-[rgb(88,75,171)] text-white text-md mt-4"
                                    :disabled="estLoading"
                                >
                                    <Loader2 v-if="estLoading" class="animate-spin h-4 w-4 mr-2"/>
                                    <span v-if="estLoading">Enviando...</span>
                                    <span v-else>Enviar solicitud</span>

                                </Button>
                                
                        </form>
                    </div>
                </div>
            </div>
        </section>

        <footer class="w-full bg-gray-900 text-gray-300 py-12">
            <div class="flex flex-col md:flex-row md:justify-around gap-8 max-w-3xl mx-auto">

                <div class="space-y-4 text-center md:text-left">

                    <h3 class="text-xl font-bold text-white">Información de Contacto</h3>
                        
                    <div class="space-y-2">
                        <p class="flex items-center gap-2 justify-center md:justify-start">
                            <Phone class="w-5 h-5"/>
                            +1 (555) 123-4567

                        </p>
                        <p class="flex items-center gap-2 justify-center md:justify-start">
                            <Mail class="w-5 h-5"/>
                            batman@wayneenterprises.com

                        </p>
                        <p class="flex items-center gap-2 justify-center md:justify-start">
                            <MapPin class="w-5 h-5"/>
                            Wayne Manor, Gotham City

                        </p>
                    </div>
                </div>

                <!-- Redes sociales -->
                <div class="space-y-4 text-center md:text-left text-gray-400">
                    <h3 class="text-xl font-bold text-white">Síguenos</h3>
                    <div class="flex gap-8 justify-center">
                        <X class="w-5 h-5"/>
                        <Instagram class="w-5 h-5"/>
                        <Linkedin class="w-5 h-5"/>
                        <MessageCircle class="w-5 h-5"/>
                        
                            
                    </div>
                </div>
            </div>
        </footer>

    </div>

</template>

<style scoped></style>