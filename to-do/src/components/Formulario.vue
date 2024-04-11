<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefasTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefasTemp" @change="props.editaTarefaTemp" required
                    type="text" placeholder="Digite a tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary">Submit</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" name="" id="" class="form-control">
                    <option value="todas">Todas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>