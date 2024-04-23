<script setup lang="ts">
import { ref, computed } from 'vue';

const cpf = ref()
const token = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzEzOTE0NDQ5LCJpYXQiOjE3MTM5MTI2NDksImp0aSI6ImNhYjg1NDc4MGZlMjRkOGY5ZGE0YzE4ZmI1Yzc4ZjJjIiwidXNlcl9pZCI6Mn0.21n272m2zHMRfX2h_ZtXpE0XVcnse_fhPTSUbYL8GnU'

const endpoint = computed(() => {
    return `api/v1/sessao/cpf/${cpf.value}`
})

const { data: sessions, status, refresh } = await useMyFetch(endpoint, {
    immediate: false,
    watch: false,
    headers: {
        "Content-Type": "application/json",
        "Authorization": "Bearer " + token
    },
    onResponse({ response }) {
        items.value = response._data.count
    }
})

const itemsPerPage = 6;

const items = ref(0);
const page = ref(1);

// const startIndex = computed(() => (page.value - 1) * itemsPerPage);
// const endIndex = computed(() => Math.min(startIndex.value + itemsPerPage, items.value));

const cpfCheck = async(c: string) => {
    cpf.value = c
    refresh()
}

</script>

<template>
    <SearchBar @search-cpf="cpfCheck" :loadStatus="status" />
    <div v-if="status === 'idle'"></div>
    <div v-else-if="status === 'pending'">
        <div class="flex items-center text-center justify-center text-4xl">
            LOADING
        </div>
    </div>
    <div v-else-if="sessions && status ==='success'">
        <div class="grid sm:grid-cols-1 md:grid-cols-1 xl:grid-cols-3 flex justify-center items-center">
            <div v-for="session in sessions.results" :key="session.id" class="py-4 px-8">
                <UCard>
                    <template #header>
                        <div class="flex justify-between items-center">
                            <div class="uppercase font-bold text-xs">
                                {{ session.especialidade }}
                            </div>
                            <div class="relative">
                                <UBadge :color="session.sessao_finalizda ? 'green' : 'red'" class="absolute top-0 right-0 -mt-3">
                                    {{ session.sessao_finalizada ? "Encerrada" : "Aberta" }}
                                </UBadge>
                            </div>
                        </div>
                    </template>
                    <div class="text-sm tracking-tight">
                        <p>
                            <span class="font-bold">Período:</span> De {{ session.dt_inicio_sessoes }} até {{ session.dt_esperada_retorno }}
                        </p>
                        <p>
                            <span class="font-bold">Consultas realizadas:</span> {{ session.num_consultas }}/20
                        </p>
                    </div>
                    <template #footer>
                        <div class="flex items-center justify-center">
                            <UButtonGroup size="md" orientation="horizontal">
                                <UTooltip text="Registrar data de consulta">
                                    <UButton icon="i-heroicons-calendar" />
                                </UTooltip>
                                <UTooltip text="Ver consultas registradas">
                                    <UButton icon="i-heroicons-eye"  />
                                </UTooltip>
                                <UTooltip text="Ver plano de desenvolvimento">
                                    <UButton icon="i-heroicons-document-text" />
                                </UTooltip>
                            </UButtonGroup>
                        </div>
                    </template>
                </UCard>
            </div>
            <div>
            </div>
        </div>
        <UContainer class="flex justify-center items-center">
            <UPagination v-model="page" :page-count="itemsPerPage" :total="items" show-first show-last/>
        </UContainer>
    </div>
</template>