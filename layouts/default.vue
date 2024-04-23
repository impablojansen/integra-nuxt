<script setup lang="ts">
const loginItems = [
    [{
        label: 'Alterar senha',
        icon: 'i-heroicons-lock-closed',
        click: () => {
            console.log("Alterar senha")
        }
    }], 
    [{
        label: 'Sair',
        icon: 'i-heroicons-arrow-left-on-rectangle'
    }]
]

const menuItems = [
    [{
        label: 'Novo Cadastro',
        icon: 'i-heroicons-user-plus',
        to: '/cadastro/novo'
    },
    {
        label: 'Editar Cadastro',
        icon: 'i-heroicons-pencil-square',
        to: '/cadastro/editar'
    }], [{
        label: 'Sessões',
        icon: 'i-heroicons-document-duplicate',
        to: '/sessoes'
    },
    {
        label: 'Lista de espera',
        icon: 'i-heroicons-clock',
    },
    {
        label: 'Baixar planilha',
        icon: 'i-heroicons-arrow-down-tray',
    }], [{
        label: 'Sair',
        icon: 'i-heroicons-arrow-left-on-rectangle'
    }]
]

</script>

<template>
    <UNotifications />
    <div class="flex bg-gray-200 flex-col h-screen">
        <nav class="bg-cyan-700 px-8 py-4">
            <div class="px-2 flex justify-between items-center">
                <img src="/public/CascavelBranco.png" class="h-16 hidden lg:block" />
                <img src="/public/Cascavel01.png" class="h-16 w-16 lg:hidden" />
                <img src="/public/logo1branco.png" alt="Logo Integra TEA" class="h-16 hidden lg:block" />
                <img src="/public/LOGO3.png" alt="Logo Integra TEA" class="h-16 w-16 lg:hidden" />
                <div class="justify-center text-center w-80 max-w-80">
                    <UDropdown :items="loginItems" :popper="{ placement: 'bottom-start' }">
                        <UButton class="text-white font-bold" color="black" label="PABLO JANSEN DE QUEIROZ MAIA" variant="ghost" trailing-icon="i-heroicons-chevron-down-20-solid" />
                    </UDropdown>
                </div>
            </div>
        </nav>
        <!-- <span class="bg-red-600 w-full h-1"/>
        <span class="bg-green-600 w-full h-1"/>
        <span class="bg-yellow-400 w-full h-1"/> -->

        <main class="flex flex-1">
            <nav class="pt-4 w-64 bg-gray-100 items-center p-2">
                <UVerticalNavigation :links="menuItems" :ui="{
                    padding: 'p-4 ps-8',
                    active: 'text-gray-900 before:bg-gray-300'
                }" />
            </nav>

            <!-- Conteúdo principal -->
            <div class="flex-1 p-2">
                <div class="rounded-md h-full shadow-2xl bg-gray-100">
                    <slot />
                </div>
            </div>
    </main>
    </div>
</template>