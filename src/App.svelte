<!-- App.svelte -->
<script lang="ts">
  import { Validators } from './lib/Validators';
  import Form from './lib/Form.svelte';
  import Input from './lib/Input.svelte';
  import Error from './lib/Error.svelte';
  import Select from './lib/Select.svelte';

  let form = {
    name: {
      validators: [Validators.required],
    },
    food: {
      validators: [Validators.required],
    },
  };

  let formEl;

  function onSubmit(e) {
    if (e?.detail?.valid) {
      console.log(e.detail.data);
      setTimeout(() => formEl.reset(), 1000)
    } else {
      console.log('Invalid Form');
    }
  }
</script>

<main>
  <Form {form} on:submit={onSubmit} bind:this={formEl}>
    <div>
      <Input label="Name" name="name" />
      <Error
        fieldName="name"
        errorKey="required"
        message="Name is required"
      />
    </div>
    <div>
      <Input label="Password" name="password" />
      <Error
        fieldName="password"
        errorKey="required"
        message="Password is required"
      />
      <Error fieldName="password" errorKey="minLength" />
    </div>
    <div>
      <Select label="Favorite food" name="food">
        <option value="chocolate">Chocolate</option>
        <option value="pizza">Pizza</option>
      </Select>
    </div>
    <button type="submit">Submit</button>
  </Form>
</main>

<style>
  * {
    box-sizing: border-box;
  }
</style>
