<template>
  <form @submit="onSubmit">
    <h5>Create a new measuring serie</h5>
    <editor-serie :editor-form="editorFormRef"></editor-serie>
    <button class="btn btn-primary" type="submit" id="submit">Add</button>
    <button class="btn secondary" type="reset" id="cancel" @click="onCancel">Abbrechen</button>
  </form>
</template>

<script>
import { CreateSerieController } from './controller';
import EditorSerieComponent from '../editor/component.vue';
import { ref } from 'vue';

export default {
  components: {
    'editor-serie': EditorSerieComponent,
  },
  setup() {
    const $ctrl = new CreateSerieController();
    const editorFormRef = ref($ctrl.editorForm);

    const onCancel = (event) => {
      $ctrl.onCancel();
    };
    const onSubmit = (event) => {
      event.preventDefault();
      event.stopPropagation();
      $ctrl.onSubmit();
      editorFormRef.value = $ctrl.editorForm;
    };

    return {
      editorFormRef,
      onCancel,
      onSubmit,
    };
  },
};
</script>
