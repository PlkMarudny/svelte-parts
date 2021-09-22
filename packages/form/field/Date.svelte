<script>
  export let field
  export let onChange

  let pristine = true
  let value = field.value

  const handleKeydown = () => {
		if (event.code == 'Enter' || event.code == 'NumpadEnter') {
			event.preventDefault()
			event.target.value
			value = event.target.value
			return false
		}
	}
</script>

<div class="field date-field {pristine ? 'pristine' : ''}">
  <label for={field.property}>{ field.label || field.property }</label>
  <input
    type="date"
    id={field.property}
    name={field.property}
    value={value}
    min={field.min}
    max={field.max}
    required={!field.notRequired}
    on:blur={() => pristine = false}
    on:keyup={() => pristine = false}
    on:keydown={handleKeydown}
    on:change={e => {
      value = e.currentTarget.value
      onChange(field.property, value)
    }}
  />
</div>