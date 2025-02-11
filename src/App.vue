<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

  //Estados Reativos Array
  const estado = reactive({
    filtro: 'todas',
    tarefaTemp:'',
    tarefas:[{
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
      titulo: 'Ir para a academia',
      finalizada: true,
    }
  ]
  })
   //Tarefas Finalizadas
   const getTarefasFinalizadas = () => {
     return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  //Tarefas Pendentes
  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)

  }


  //Tarefas Filtradas
  const getTarefasFiltradas = () => {
    const {filtro} = estado;

    switch(filtro){
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;

    }
  }

  const cadastrarTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
    
  }


</script>

<template>
  <div class="container">
    <Cabecalho  :tarefasPendentes="getTarefasPendentes().length"/>
    <Formulario :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastrarTarefa" :trocar-filtro="evento => estado.filtro = evento.target.value"/>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
    
  </div>
  
</template>


