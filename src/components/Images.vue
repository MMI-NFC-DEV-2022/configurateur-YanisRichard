<script setup lang="ts">
import type { ChaussureImage } from '@/types-images';

withDefaults(defineProps<ChaussureImage>(), {
    orientation: "cote",
    bandes: "bleu",
    cuir: "bleu",
    mousse: "bleu"
});
</script>

<template