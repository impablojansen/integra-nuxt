<script setup lang="ts">
definePageMeta({
    layout: 'custom'
})

const state = reactive({
    username: undefined,
    password: undefined
})

const isVisible = ref(false)
const passwordVisible = computed(() => {
    return isVisible.value ? "text" : "password"
})

function displayPassword() {
    isVisible.value = !isVisible.value
}

const { data: profile, status, refresh, execute } = await useFetch("api/token/", {
    immediate: false,
    watch: false,
    body: {
        "username": state.username,
        "password": state.password
    },
    onResponse({ response }) {
        console.log(response)
    }
})

async function handleLogin () {
    console.log(state.username, state.password)
    refresh()
}

</script>

<template>
    <div class="flex justify-center bg-cyan-600 items-center h-screen text-center">
        <UCard :ui="{ body: { base:'grid grid-cols-5' } }">
            <div class="space-y-4 justify-center items-center flex col-span-2">
                <NuxtImg src="/logo2.png" sizes="md:200px" />
            </div>
            <UDivider orientation="vertical" class="col-span-1"/>
            <div class="flex flex-col justify-center col-span-2">
                <span class="font-bold text-center py-2">
                    Bem vindo(a)! Faça seu login:
                </span>
                <UForm @submit="handleLogin" :state="state" class="space-y-4">
                    <UFormGroup label="Usuário" required >
                        <UInput
                            v-model="state.username"
                            name="username"
                            icon="i-heroicons-user"
                            placeholder="Digite seu login"
                            autocomplete="off"
                        />
                    </UFormGroup>
                    <UFormGroup label="Senha" required>
                        <UInput
                            v-model="state.password"
                            name="password"
                            placeholder="Digite sua senha"
                            icon="i-heroicons-lock-closed"
                            autocomplete="off"
                            :ui="{ icon: { trailing: { pointer: '' } } }"
                            :type="passwordVisible"
                        >
                    <template #trailing>
                        <UButton v-show="state.password != ''" icon="i-heroicons-eye-slash" variant="link"
                        :padded="false"
                        @click="displayPassword"
                        >
                        </UButton>
                    </template>
                    </UInput>
                    </UFormGroup>
                    <UButton label="Entrar" />
                </UForm>
            </div>
        </UCard>
    </div>
</template>