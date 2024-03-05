<script setup lang="ts">
import {ref} from "@vue/reactivity";
import AfficheMaison from "@/components/AfficheMaison.vue";
import type { SchemaOffreMaison } from "@/type";

const maison =ref<SchemaOffreMaison>({});

async function upsertMaison(dataForm, node) {
 const { data, error } = await supabase.from("Maison").upsert(dataForm).select("id");
 if (error) node.setErrors([error.message])
 else {
console.log("data : ", data)}
}

</script>
<template>
    <div>
        <div class="p-2">
            <h2 class="text-2xl">Résultat</h2>
            <AfficheMaison v-bind="maison"/>
        </div>
    </div>
    <div>
         <FormKit 
            type="form" 
            v-model="maison"
            :submit-attrs="{ classes: { input: 'bg-red-300 p-1 rounded' } }"
            @submit="upsertMaison"
        >
            <FormKit name="nomMaison" label="nom"></FormKit>
            <FormKit name="prix" label="prix" type="number"></FormKit>
            <FormKit name="favori" label="mettre en valeur" type="checkbox"></FormKit>
           
        </FormKit> 
    </div>
</template>