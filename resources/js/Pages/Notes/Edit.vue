<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import { useForm } from '@inertiajs/vue3'

 
const props = defineProps({
  note: Object
})

const form = useForm({
    excerpt:props.note.excerpt,
    content:props.note.content
});

const submit = () => {
    form.put(route('notes.update',props.note.id), form);
};

const destroy = ( id ) => {
    if( confirm('Esta seguro de eliminar esta Nota ?') ) {
        
        form.delete(route('notes.destroy',props.note.id))

        //useForm({}).delete(route('notes.destroy', id));
    }
}

</script>


<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
            </h2>
                Módulo de Notas
        </template>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="md:grid md:grid-cols-3 md:gap-6">
                    <div class="md:col-span-1">
                        <div class="px-4 sm:px0">
                            <h3 class="text-lg text-gray-900">Editar una nota</h3>
                            <p class="text-sm text-gray-600">Si editas no podrás volver al estado anterior</p> 
                        </div>
                    </div>
                    <div class="md:col-span-2 mt-5 md:mt-0">
                        <div class="shadow bg-white md:rounded-md p-4">
                            <form @submit.prevent="submit">
                        
                                <label class="block font-medium text-sm text-gray-700">
                                    Resumen
                                </label>
                               <textarea 
                                    class="form-input w-full rounded-md shadow-sm"
                                    v-model="form.excerpt">
                                </textarea>
                                <label class="block font-medium text-sm text-gray-700">
                                    Contenido
                                </label>      
                                <textarea 
                                    class="form-input w-full rounded-md shadow-sm"
                                    v-model="form.content"
                                    rows="8">
                                </textarea>
                                <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-md">
                                    Editar
                                </button>             
                            </form>
                            <hr class="my-6">

                            <a href="#" @click.prevent="destroy">
                                Eliminar Nota
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </AppLayout>
</template>
