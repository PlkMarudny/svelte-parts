<script>
  import { createEventDispatcher } from 'svelte'
  import getInitialData from './getInitialData'
  import RenderField from './field/index.svelte'

  export let fields = []
  export let onSubmit = undefined
  export let onSaveAsNew = undefined
  export let submitButton = undefined
  export let submitAsButton = undefined
  export let errorMessage = undefined
  
  const dispatch = createEventDispatcher();

  let data = getInitialData(fields)

  const setData = (key, value) => {
    data = { ...data, [key]: value }
    dispatch('isdirty');
  }

  const onNativeSubmit = e => {
    e.preventDefault()
    if (e.currentTarget.checkValidity() && onSubmit) {
      onSubmit(data)
    }
  }

  const onSubmitAsNew = e => {
    e.preventDefault()
    if (e.currentTarget.checkValidity() && onSubmit) {
      onSaveAsNew(data)
    }
  }

</script>

<form on:submit|preventDefault={onNativeSubmit} action="#" autocomplete="off">
  {#each fields as field }
    <RenderField field={field} onChange={setData} />
  {/each}
  {#if errorMessage}
    <p class="error-message">{ errorMessage }</p>
  {/if}
  <div class="field submit-field">
    {#if submitButton}
      <input type="submit" value={submitButton} />
    {:else}
      <input type="submit" />
    {/if}
    {#if submitAsButton}
      <input type="submit" value={submitAsButton} on:click={onSubmitAsNew} />
    {/if}
  </div>
</form>
