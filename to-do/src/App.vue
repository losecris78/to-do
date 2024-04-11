<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';


const estado = reactive({
  filtro: 'todas',
  tarefasTemp: '',
  tarefas:[
    {
      titulo: 'Estudar ingles',
    finalizada: false,
    },
    {
      titulo:'Estudar as escrituras',
      finalizada:false,
    },
    {
      titulo:'Practicar digitacao',
      finalizada: true,
    },
  ]
})
const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}
const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}
const getTarefasFiltradas = () =>{
  const {filtro} = estado;
  switch (filtro){
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}
const cadastraTarefa = ()=>{
  const tarefaNova = {
    titulo: estado.tarefasTemp,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefasTemp= '';
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes = "getTarefasPendentes().length "/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefas-temp="estado.tarefasTemp" :edita-tarefa-temp ="evento => estado.tarefasTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/> 
  </div>
</template>

