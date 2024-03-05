<script setup lang="ts">
import { ref } from 'vue';
import { supabase } from '@/supabase';
import { FormKit } from '@formkit/vue';
import { type Tables } from '@/supabase-types';
console.log("supabase :", supabase);

const quartier =ref<Tables<"Quartier">>({});

async function upsertQuartier(dataForm, node) {
    console.log("On affiche dataform:", dataForm);
    
 const { data, error } = await supabase.from("Quartier").upsert(dataForm).select("id");
    console.log("Résultat de l'insertion" , {data, error})
 if (error) node.setErrors([error.message])
 else {
console.log("data : ", data)}
}
  
</script>

<template>
    <div>
        <FormKit 
            type="form" 
            v-model="quartier"
            :submit-attrs="{ classes: { input: 'bg-red-300 p-1 rounded' } }"
            @submit="upsertQuartier"
        >
            <FormKit name="nom_quartier" label="Nom Quartier" />
            <FormKit name="id_Commune" label="ID Commune" />
        </FormKit> 
    </div>
</template>