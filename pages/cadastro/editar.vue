<script setup lang="ts">
const cpf = ref()
const patientData = ref()

const token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzEzODg0MjEyLCJpYXQiOjE3MTM4ODI0MTIsImp0aSI6IjRhZTg0YTMzZDc4MDQxOGI5MjA3ZDZlYjZhN2E0ZDFkIiwidXNlcl9pZCI6Mn0.RF0mznEdUrLibLdR18VmmRo0cZjIgg6fhCkX8kJgte0"

const endpoint = computed(() => {
    return `http://127.0.0.1:8000/api/v1/crianca/${cpf.value}`
})

const toast = useToast()

const { data, status, refresh, error } = await useFetch(endpoint, {
    immediate: false,
    watch: false,
    headers: {
        "Content-Type": "application/json",
        "Authorization": "Bearer " + token
    },
    onResponse({ response }) {
        patientData.value = response._data
    },
    onResponseError({ response }) {
        if (response.status === 401) {
            toast.add(({
                title: "Erro",
                description: response._data.detail,
                color: 'red',
                icon: 'i-heroicons-x-circle'
            }))
        }
        console.log(response)
    }
})

const cpfCheck = async(c: string) => {
    cpf.value = c
    await refresh()
}

</script>

<template>
    {{ status }}
    {{  error }}
        <SearchBar @search-cpf="cpfCheck" :loadStatus="status" />
        <div v-if="status === 'idle'"></div>
        <div v-if="status === 'pending'">
            LOADING
        </div>
        <div class="w-full text-center items-center uppercase font-bold text-2xl">
            Editar cadastro
        </div>
        <FormsPatientForm btn-text="Editar Cadastro" :patient-data="patientData" />
</template>