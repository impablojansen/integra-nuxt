<script setup lang="ts">
const props = defineProps({
    btnText: {
        type: String,
        required: true,
    },
    patientData :{
        type: Object,
        required: false,
    }
})

const pAquarela = ref(false)
const pRecrearte = ref(false)
const pPiabinha = ref(false)
const laudo = ref(false)
const localTerapia = ref('PUBLICA')
const options = [{
    name: 'Rede pública',
    value: 'PUBLICA',
    }, {
    name: 'Rede privada',
    value: 'PRIVADA',
}]

const test = async() => {
    console.log(props.patientData)
}

</script>

<template>
    {{ patientData }}
    <div class="p-8" >
            <UForm >
                <div class="grid sm:grid-cols-1 md:grid-cols-1 lg:grid-cols-4 gap-y-4 gap-x-2 md:gap-x-8 lg:gap-x-6">
                    <UFormGroup label="Nome do paciente" name="nome" class="col-span-1 md:col-span-2" >
                        <UInput />
                    </UFormGroup>
                    <UFormGroup label="CPF do paciente" name="cpf"  >
                        <UInput />
                    </UFormGroup>
                    <UFormGroup label="Data de Nascimento" name="nasc" >
                        <UInput type="date"/>
                    </UFormGroup>
                    <UFormGroup label="Nome do(a) responsável" name="nome_resp" class="col-span-1 md:col-span-2">
                        <UInput />
                    </UFormGroup>
                    <UFormGroup label="CPF do responsável" name="cpf_resp" >
                        <UInput />
                    </UFormGroup>
                    <UFormGroup label="Telefone de contato" name="telefone" >
                        <UInput />
                    </UFormGroup>
                </div>
                <UDivider class="py-6" :ui="{ border: { base: 'border-gray-300' }}" />
                <div class="grid sm:grid-cols-1 md:grid-cols-1 lg:grid-cols-4 gap-y-4 gap-x-2 md:gap-x-8 lg:gap-x-6">
                    <UFormGroup label="Logradouro" name="logradouro" >
                        <UInput />
                    </UFormGroup>
                    <UFormGroup label="Número" name="num_log"  >
                        <UInput />
                    </UFormGroup>
                    <UFormGroup label="Complemento" name="complemento" >
                        <UInput />
                    </UFormGroup>
                    <UFormGroup label="Bairro" name="bairro" >
                        <UInput />
                    </UFormGroup>
                    <UFormGroup label="Escola" name="escola" >
                        <UInput />
                    </UFormGroup>
                    <UFormGroup label="CID" name="cid" >
                        <UInput />
                    </UFormGroup>
                    <UFormGroup label="Local de terapia" name="local_terapia" >
                        <USelect v-model="localTerapia" :options="options" option-attribute="name"/>
                    </UFormGroup>
                    <UFormGroup class="flex items-center">
                        <UCheckbox v-model="laudo" label="Paciente com laudo" :ui="{ base: 'h-6 w-6' }" />
                    </UFormGroup>
                </div>
                <UDivider label="Projetos" class="py-4" :ui="{ border: { base: 'border-gray-300' }}" />
    
                <div class="sm:px-4 px-24 items-center flex justify-around sm:grid-cols-1 md:grid-cols-1 lg:grid-cols-3 gap-y-4 gap-x-2 md:gap-x-8 lg:gap-x-6">
                    <UFormGroup label="Aquarela das artes" >
                        <UCheckbox v-model="pAquarela" class="justify-center pt-2" :ui="{ base: 'h-6 w-6' }" />
                    </UFormGroup>
                    <UFormGroup label="Piabinha">
                        <UCheckbox v-model="pPiabinha"  class="justify-center pt-2":ui="{ base: 'h-6 w-6' }" />
                    </UFormGroup>
                    <UFormGroup label="Recrearte">
                        <UCheckbox v-model="pRecrearte" class="justify-center pt-2" :ui="{ base: 'h-6 w-6' }" />
                    </UFormGroup>
                </div>
                <div class="pt-8 flex text-center justify-center items-center">
                    <UButton @click="test" :label="btnText" />
                </div>
            </UForm>
        </div>
</template>