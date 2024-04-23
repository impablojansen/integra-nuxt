<script setup lang="ts">
import { ref } from 'vue';
const props = defineProps({
    loadStatus: {
        type: String,
        default: 'idle'
    }
})

const cpf = ref("")
const loading = computed(() => {
    return props.loadStatus === 'pending' ? true : false
})

const emit = defineEmits(['search-cpf'])

async function handleSearchCpf() {
    if (cpf.value.length < 11) {
        console.log("CHAMA O TOAST")
    } else {
       emit('search-cpf', cpf.value)
    }
}

const handleKeyDown = ((e: KeyboardEvent) => {
    const isNumber = (e.key >= '0' && e.key <= '9') || ['Backspace', 'Delete', 'ArrowLeft', 'ArrowRight', 'Enter'].includes(e.key);
    if (!isNumber) {
        e.preventDefault()
    }
    cpf.value = cpf.value.replace(/\D/g, "")
})
</script>

<template>
    <div class="w-full">
        <div class="w-80 py-4 px-8">
            <form @submit.prevent="handleSearchCpf">
                <UInput 
                    v-model="cpf" 
                    name="cpf"
                    placeholder="Buscar por CPF..." 
                    icon="i-heroicons-magnifying-glass-20-solid" 
                    autocomplete="off"
                    :loading=loading
                    :maxlength="11" 
                    :ui="{ icon: { trailing: { pointer: '' } } }"
                    @keydown="handleKeyDown"
                >
                <template #trailing>
                    <UButton 
                        v-show="cpf !== ''"
                        color="gray"
                        variant="link"
                        icon="i-heroicons-x-mark-20-solid"
                        :padded="false"
                        @click="cpf = ''"
                    />
                </template>
                </UInput>
            </form>
        </div>
    </div>
</template>