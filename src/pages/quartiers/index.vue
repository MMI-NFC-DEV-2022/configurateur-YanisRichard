<script setup lang="ts">
import { RouterLink } from "vue-router";
import { supabase } from "@/supabase";
import type { Database } from "@/supabase-types";
import { useRouter } from "vue-router";
// let { data, error } = await supabase
//   .from('quartier_commune')
//   .select()

//   console.log("Quartier commune : ",data);

const {data, error} = await supabase.from("Commune").select(`
  *,
  Quartier(*)
`);
console.log("les quarties par commune : ",data);

  
if (error) console.log("n'a pas pu charger la table quartiercommune :", error);

let idQuartierASupprimer = 0 ; 
const router= useRouter();
async function supprimerQuartier() {
    console.log("supprimerQuartier", idQuartierASupprimer);
  const { data, error } = await supabase
    .from("Quartier")
    .delete()
    .match({ id: idQuartierASupprimer });
    console.log("data :", data, "error :", error);
    
  if (error) {
    console.error(
      "Erreur à la suppression de ",
      idQuartierASupprimer,
      "erreur :",
      error
    );
  } else {
    router.push({ name: "/quartiers/",force:true});
  }
}

</script>

<template>
  <!--<section class="flex flex-col">
 <h3 class="text-2xl">Liste des quartiers</h3>
    <ul>
      <li v-for="quartierObject in data ">
        {{ quartierObject.nom_commune }} -
        {{ quartierObject.nom_quartier }}
      </li>
    </ul>
  </section> -->

  <h3>Liste des Quartiers Simplifié </h3>

  <section class="flex flex-col">
    <h3 class="text-2xl">Liste des quartiers</h3>
    <ul>
      <li v-for="Commune in data" :key="Commune.id">
        {{ Commune.nom_commune }} 
        <ul>
            <li v-for="Quartier in (Commune.Quartier)" :key="Quartier.id">
                <RouterLink :to="{name:'/quartiers/edit/[[id]]', params:{id:Quartier.id}}"> 
                    {{ Quartier.nom_quartier }} 
                </RouterLink> 
                <button
                    type="button"
                    @click="($refs.dialogSupprimer as any).showModal(); idQuartierASupprimer = Quartier.id"
                    class="focus-style justify-self-end rounded-md bg-red-500 p-2 shadow-sm"
                >       
                    Supprimer l'offre
                </button>
            </li>
            </ul>


    
      

      </li>
    </ul>

    <dialog
        ref="dialogSupprimer"
        @click="($event.currentTarget as any).close()"
      >
        <button
          type="button"
          class="focus-style justify-self-end rounded-md bg-blue-300 p-2 shadow-sm"
        >
          Annuler</button
        ><button
          type="button"
          @click="supprimerQuartier()"
          class="focus-style rounded-md bg-red-500 p-2 shadow-sm"
        >
          Confirmer suppression
        </button>
      </dialog>
  </section>
</template>