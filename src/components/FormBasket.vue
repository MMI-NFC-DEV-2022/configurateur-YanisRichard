<script setup lang="ts">
import type { Basket } from '@/types';
import { ref } from 'vue';
import SvgProfil from './BasketProfil.vue';
import SvgDessus from './BasketDessus.vue';

const props = defineProps<{
  data?: Basket;
  id?: string;
}>();

const chaussure = ref<Basket>(props.data ?? {});
</script>

<template>
    <div class="p-2">
        <ul class="flex gap-10">
            <li><a href="#profil">Profil</a></li>
            <li><a href="#dessus">Dessus</a></li>
        </ul>
    </div>
    <div class="carousel w-64">
        <SvgProfil class="carousel-item w-64" v-bind="chaussure" id="profil" />
        <SvgDessus class="carousel-item w-64" v-bind="chaussure" id="dessus" />        
    </div>
    <FormKit type="form" v-model="chaussure">
        <FormKit name="semelle" label="semelle" value="#FFFFFF" type="color" />
        <FormKit name="empeigne" label="empeigne" value="#FFFFFF" type="color" />
        <FormKit name="pointe" label="pointe" value="#FFFFFF" type="color" />
        <FormKit name="oeillet" label="oeillet" value="#FFFFFF" type="color" />
        <FormKit name="bande" label="bande" value="#FFFFFF" type="color" />
        <FormKit name="languette" label="languette" value="#FFFFFF" type="color" />
        <FormKit name="lacet" label="lacet" value="#FFFFFF" type="color" />
        <FormKit name="trimestre" label="trimestre" value="#FFFFFF" type="color" />
    </FormKit>

</template>./BasketProfil.vue@/types