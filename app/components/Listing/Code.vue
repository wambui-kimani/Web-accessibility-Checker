<script setup lang="ts">
import type { NodeResult } from 'axe-core';

const { $highlighter, $format } = useNuxtApp()

const props = defineProps<{
    node: NodeResult
}>()

function highlight(code: string) {
    return $highlighter.codeToHtml(code, {
        lang: 'html',
        theme: 'light-plus'
    });
}


const code = highlight(await $format(props.node.html).catch(_ => props.node.html))
</script>
<template>
    <small style="font-size: 10px;"><span class="uppercase font-bold">
            X-Path:</span> {{ node.xpath }}
    </small>
    <p class="p-1" v-html="code"></p>
</template>