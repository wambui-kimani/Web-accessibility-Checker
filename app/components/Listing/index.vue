<script setup lang="ts">
import type { Result } from "axe-core"
const button = ref<HTMLDivElement | null>(null)
defineProps<{
    listing?: Result,
    index: number,
    tab: "incomplete" | "inapplicable" | "critical" | "pass"
}>()

const emits = defineEmits<{
    "view-details": [],
    "hide-details": []
}>()

let detailsShown = false
function toggleDetails() {
    if (!detailsShown) {
        emits('view-details')
        button.value?.classList.add('rotate')
    } else {
        emits('hide-details')
        button.value?.classList.remove('rotate')
    }
    detailsShown = !detailsShown
}
</script>

<template>
    <td class="text-center align-top pt-2.5">{{ index + 1 }}</td>
    <td class="p-2">{{ listing?.help }}</td>
    <td class="max-sm:hidden">
        <ListingTags :tags="listing?.tags" />
    </td>
    <td>
        <div class="justify-center flex items-center" @click="toggleDetails" v-if="tab !== 'inapplicable'">
            <div class="flex w-fit bg-white rounded-full p-2 cursor-pointer transition-transform" ref="button">
                <svg width="10" height="6" viewBox="0 0 10 6" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M4.99998 3.87855L8.71233 0.16626L9.77298 1.22692L4.99998 5.99993L0.227051 1.22692L1.28771 0.16626L4.99998 3.87855Z"
                        fill="black" />
                </svg>
            </div>
        </div>
    </td>
</template>

<style scoped>
.rotate {
    transform: rotate(180deg);
}
</style>