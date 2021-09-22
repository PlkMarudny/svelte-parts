<script>
  export let field
  export let onChange

  let pristine = true
  let value = field.value || ''

  let onValueChange = (event, key, value) => {
    pristine = false
    onChange(key, value)
  }

  const handleKeydown = () => {
		if (event.code == 'Enter' || event.code == 'NumpadEnter') {
			event.preventDefault()
			event.target.value
			value = event.target.value
			return false
		}
	}
</script>

<div class="field text-field {pristine ? 'pristine' : ''}">
  <label for={field.property}>{ field.label || field.property }</label>
  <input autocomplete="off"
    type={field.type}
    id={field.property}
    name={field.property}
    value={value}
    minlength={field.minLength}
    maxLength={field.maxLength}
    pattern={field.pattern}
    required={!field.notRequired}
    on:blur={e => { onValueChange(e, field.property, e.currentTarget.value) }}
    on:keydown={handleKeydown}
    on:keyup={e => { onValueChange(e, field.property, e.currentTarget.value) }}
    placeholder={field.placeholder}
  />
</div>