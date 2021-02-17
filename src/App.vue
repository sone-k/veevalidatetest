<template>
  <div>
    <Form v-slot="{ errors }" :validation-schema="schema" :validateOnMount="true">
      <div>rules: </div>
      <div>1. check is required</div>
      <div>2. at least 2 items are checked</div>
      
      <div style="margin-top:20px;">
        <span>item1: </span>
        <Field
          as="input"
          type="checkbox"
          name="sample"
          value="1"
          v-model="state.array"
        />
      </div>
      <div>
        <span>item2: </span>
        <Field
          as="input"
          type="checkbox"
          name="sample"
          value="2"
          v-model="state.array"
        />
      </div>
      <div>
        <span>item3: </span>
        <Field
          as="input"
          type="checkbox"
          name="sample"
          value="3"
          v-model="state.array"
        />
      </div>
      
      <ErrorMessage as="div" name="sample" style="color:red;"/>
      <div style="color:red;">errors: {{ errors }}</div>
    </Form>
    <div v-for="(val, key) in state.array" :key="key">{{val}} is checked</div>
    <div style="margin-top:20px;">result on schema: <b>{{ state.isValid }}</b></div>
  </div>
</template>

<script>
import { reactive } from 'vue'
import { Form, Field, ErrorMessage } from 'vee-validate'

export default {
  name: 'App',
  components: {
    Form,
    Field,
    ErrorMessage
  },
  setup () {
    const state = reactive({
      array: [],
      isValid: null,
    })
    const schema = {
      sample: (value) => {
        state.isValid = false
        if (!value.length) {
          return true
        }
        if (value.length < 2) {
          return 'please check at least 2 items'
        }
        state.isValid = true
        return true
      }
    }
  
    return {
      state,
      schema
    }
  }
}
</script>

<style></style>
