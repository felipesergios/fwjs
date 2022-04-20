<template>
  <div className="tabsPane">
    <h1>TabComponent</h1>
    
    <button v-for="(option, index) in contents_tabs" :key="index"
      :class="{ selected: index === index }"
      @click="$emit(currentQuestion=index)">
      {{ option.index }}
    </button>

        

           <div class="questionPane">
        <div className="questionNumber">
         <Statement
          v-bind="contents_tabs[currentQuestion]"
          :selection="currentOption"
          @on-selection="select"
          />
        </div>
        
      </div>
      
    </div>
</template>

<script setup lang="ts">
  import { ref, reactive, computed } from 'vue'
  import Statement, { type TabsProps } from './Statement.vue'
  


  const contents_tabs: TabsProps[] = [
      {
          index:1,
          content:"Conteudo do coisa 1"
      },
      {
          index:2,
          content:"Conteudo do coisa 2"
      },
      {
          index:3,
          content:"Conteudo do coisa 3"
      },
      {
          index:4,
          content:"Conteudo do coisa 4"
      },
  ]

  // estados reativos do componente
  const currentQuestion = ref(0)          // ref() é útil para tipos primitivos
  const currentOption = ref<number>()     // como a opção inicial é undefined, é interessante definir o tipo
 

  /** Atualiza a opção selecionada pelo usuário. */
  function select(optionIndex: number) {
    currentOption.value = optionIndex
     currentQuestion.value = optionIndex
  }

 

</script>

<style>
.tabsPane {
  padding: 50px;
}

.questionPane {
  padding: 20px;
  margin: 10px 0;
  border-radius: 10px;
  border: 1px solid #aaa;
  background-color: #f0f0f0;
}

.questionNumber {
  font-style: italic;
  font-size: smaller;
}
</style>