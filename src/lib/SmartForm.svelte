<script>
  import { createEventDispatcher } from 'svelte';
  
  export let fields = [];
  export let submitText = 'Submit';
  
  let formData = {};
  let errors = {};
  const dispatch = createEventDispatcher();
  
  function handleSubmit() {
    if (validateForm()) {
      dispatch('submit', formData);
    }
  }
  
  function validateForm() {
    errors = {};
    fields.forEach(field => {
      const error = validateField(field, formData[field.name]);
      if (error) {
        errors[field.name] = error;
      }
    });
    return Object.keys(errors).length === 0;
  }
  
  function validateField(field, value) {
    if (field.required && !value) return `${field.label} is required`;
    if (field.type === 'email' && !/\S+@\S+\.\S+/.test(value)) return 'Invalid email format';
    if (field.minLength && value.length < field.minLength) return `Minimum length is ${field.minLength}`;
    if (field.maxLength && value.length > field.maxLength) return `Maximum length is ${field.maxLength}`;
    if (field.pattern && !new RegExp(field.pattern).test(value)) return `Invalid format`;
    if (field.validate && typeof field.validate === 'function') {
      return field.validate(value);
    }
    return '';
  }

  function handleInput(field) {
    const error = validateField(field, formData[field.name]);
    if (error) {
      errors[field.name] = error;
    } else {
      delete errors[field.name];
    }
  }
</script>

<form on:submit|preventDefault={handleSubmit}>
  {#each fields as field}
    <div class="form-field">
      <label for={field.name}>{field.label}</label>
      
      {#if field.type === 'textarea'}
        <textarea
          id={field.name}
          bind:value={formData[field.name]}
          on:input={() => handleInput(field)}
          placeholder={field.placeholder}
          required={field.required}
        ></textarea>
      {:else if field.type === 'checkbox'}
        <input
          type="checkbox"
          id={field.name}
          bind:checked={formData[field.name]}
          on:change={() => handleInput(field)}
          required={field.required}
        />
      {:else if field.type === 'radio'}
        {#each field.options as option}
          <label>
            <input
              type="radio"
              name={field.name}
              value={option.value}
              bind:group={formData[field.name]}
              on:change={() => handleInput(field)}
              required={field.required}
            />
            {option.label}
          </label>
        {/each}
      {:else if field.type === 'select'}
        <select
          id={field.name}
          bind:value={formData[field.name]}
          on:change={() => handleInput(field)}
          required={field.required}
        >
          {#each field.options as option}
            <option value={option.value}>{option.label}</option>
          {/each}
        </select>
      {:else if field.type === 'text'}
        <input type="text" id={field.name} bind:value={formData[field.name]} on:input={() => handleInput(field)} placeholder={field.placeholder} required={field.required} />
      {:else if field.type === 'email'}
        <input type="email" id={field.name} bind:value={formData[field.name]} on:input={() => handleInput(field)} placeholder={field.placeholder} required={field.required} />
      {:else if field.type === 'number'}
        <input type="number" id={field.name} bind:value={formData[field.name]} on:input={() => handleInput(field)} placeholder={field.placeholder} required={field.required} />
      {:else if field.type === 'password'}
        <input type="password" id={field.name} bind:value={formData[field.name]} on:input={() => handleInput(field)} placeholder={field.placeholder} required={field.required} />
      {:else if field.type === 'date'}
        <input type="date" id={field.name} bind:value={formData[field.name]} on:input={() => handleInput(field)} required={field.required} />
      {:else if field.type === 'time'}
        <input type="time" id={field.name} bind:value={formData[field.name]} on:input={() => handleInput(field)} required={field.required} />
      {:else if field.type === 'tel'}
        <input type="tel" id={field.name} bind:value={formData[field.name]} on:input={() => handleInput(field)} placeholder={field.placeholder} required={field.required} />
      {:else if field.type === 'url'}
        <input type="url" id={field.name} bind:value={formData[field.name]} on:input={() => handleInput(field)} placeholder={field.placeholder} required={field.required} />
      {/if}
      
      {#if errors[field.name]}
        <span class="error">{errors[field.name]}</span>
      {/if}
    </div>
  {/each}
  <button type="submit">{submitText}</button>
</form>

<style>
  .form-field {
    margin-bottom: 1rem;
  }
  label {
    display: block;
    margin-bottom: 0.5rem;
  }
  input, textarea, select {
    width: 50%;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  input[type="checkbox"], input[type="radio"] {
    width: auto;
    margin-right: 0.5rem;
  }
  .error {
    color: red;
    font-size: 0.8rem;
  }
  button {
    background-color: #4CAF50;
    color: white;
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  button:hover {
    background-color: #45a049;
  }
</style>