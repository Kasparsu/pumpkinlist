<script setup>
import { ref, onMounted } from 'vue'

const pumpkins = ref([])

onMounted(async () => {
    const response = await fetch('https://wplace.samuelscheit.com/tiles/pumpkin.json')
    pumpkins.value = await response.json();
    pumpkins.value = Object.values(pumpkins.value).sort((a, b) => new Date(b.foundAt) - new Date(a.foundAt));
})
</script>
<template>
    <div class="container mx-auto flex justify-center w-1/2 h-full flex flex-col items-center justify-center  pt-10">
        <div v-for="(pumpkin, index) in pumpkins" :key="index" class="rounded border px-3 py-1 text-sm transition-shadow border-neutral-200 bg-white/80 w-1/2">
            <div class="flex items-center justify-between">
                <div class="flex items-center gap-2 font-semibold text-neutral-800">{{ index }}<div
                        class="text-neutral-500 text-xs font-normal">
                        <div>Found at {{pumpkin.foundAt}} AM</div>
                    </div>
                </div>
                <a :href="`https://wplace.live/?lat=${pumpkin.lat}&lng=${pumpkin.lng}&zoom=14`"
                    type="button" target="_blank" rel="noopener noreferrer"
                    class="mt-1 inline-flex items-center gap-2 rounded bg-neutral-900/80 px-3 py-1 text-xs font-semibold text-neutral-100 shadow hover:bg-neutral-800 focus-visible:outline focus-visible:outline-offset-2 focus-visible:outline-neutral-400">Open
                    live<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="size-3" aria-hidden="true">
                        <path fill="currentColor"
                            d="M432 320H416c-8.84 0-16 7.16-16 16v112H48V80h112c8.84 0 16-7.16 16-16V48c0-8.84-7.16-16-16-16H32C14.33 32 0 46.33 0 64v384c0 17.67 14.33 32 32 32h384c17.67 0 32-14.33 32-32V336c0-8.84-7.16-16-16-16zM424 0H296c-13.25 0-24 10.75-24 24v128c0 21.36 25.85 32.09 40.97 16.97l35.72-35.72L201 301.7c-6.24 6.24-6.24 16.38 0 22.62l22.63 22.62c6.25 6.24 16.38 6.24 22.63 0l147.68-147.45 35.72 35.72C335.91 249.15 346.64 224 325.28 224H456c13.25 0 24-10.75 24-24V24c0-13.25-10.75-24-24-24z">
                        </path>
                    </svg></a>
            </div>
        </div>

    </div>
</template>