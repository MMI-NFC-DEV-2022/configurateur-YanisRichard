<!-- eslint-disable vue/multi-word-component-names -->
<script setup lang="ts">
import AfficheMaison from '@/components/AfficheMaison.vue';
import { supabase } from "@/supabase";
console.log("supabase :", supabase); // pour vérifier et "garder" supabase dans le code

let { data: maisons, error } = await supabase
  .from('Maisons')
  .select('*')



</script>

<template>

    <AfficheMaison v-for="maison of maisons" v-bind="maison" :key="maison.nomMaison"/>
</template>