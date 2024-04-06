<script setup lang="ts">
import { ref } from 'vue';
import InputWithValidation from '@/components/InputWithValidation.vue';
import { useForm } from 'vee-validate';
import * as yup from 'yup';

type Form = {
  test: string,
  test2: string,
}

const model = ref<Form>({
  test: '',
  test2: ''
});

const { handleSubmit } = useForm({
  validationSchema: yup.object({
    test: yup.string().required().min(10),
    test2: yup.string().required().min(10)
  })
});

const onSubmit = handleSubmit(values => {
  alert(JSON.stringify(values, null, 2));
});

</script>

<template>
  <div class="hero min-h-screen bg-base-200">
    <div class="hero-content text-center">
      <div class="max-w-md">
        <h2 class="text-left text-3xl font-semibold pb-4">Test Form</h2>
        <form @submit.prevent="onSubmit">
          <input-with-validation name="test" id="test" label="test" v-model="model.test"
            :required="true"></input-with-validation>
          <input-with-validation name="test2" id="test2" label="test2" v-model="model.test2"></input-with-validation>
          <button class="mt-4 bg-blue-500 hover:bg-blue-600 text-white font-semibold py-2 px-4 rounded">Submit</button>
        </form>


      </div>
    </div>
  </div>

</template>
