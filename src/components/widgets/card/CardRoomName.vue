<template>
  <v-card color="#E1F5FE">
    <v-card-title>
      <span>Informe o nome da sala:</span>
    </v-card-title>
    <v-card-text>
      <v-container>
        <v-row>
          <v-col cols="12">
            <center>(caso queira entrar em uma sala, informe o mesmo nome da sala já criada).</center>
            <v-text-field
              maxlength="10"
              autofocus
              :error-messages="errorMessage"
              v-model="state.roomName"
            />
          </v-col>          
        </v-row>
      </v-container>
    </v-card-text>
    <v-card-actions>
      <div class="flex-grow-1"></div>
      <v-btn
        dark
        depressed
        color="#43B581"
        @click="searchRoom">
        CONTINUAR
      </v-btn>
      <v-btn
        dark
        depressed
        color="#FF5252"
        @click="cancel">
        CANCELAR
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script lang="ts">
import { defineComponent, reactive, } from '@vue/composition-api'

export default defineComponent({
  
  props: {
    errorMessage: {
      type: String,
      required: true,
    }
  },

  setup(props, context) {
    const state = reactive<{
      roomName: string;
    }>({
      roomName: '',
    })

    function searchRoom(): void {
      context.emit('searchRoom', state.roomName)
    }

    function cancel(): void {
      context.emit('cancel')
    }

    return {
      state,
      searchRoom,
      cancel,
    }
  }
})
</script>

<style scoped>

</style>