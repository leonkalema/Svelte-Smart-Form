<script>
    import { writable } from 'svelte/store';
    import SmartForm from './SmartForm.svelte';
  
    let fields = writable([]);
    let formName = writable('MySmartForm');
    let includeCSS = writable(true);
  
    let newField = {
      name: '',
      type: 'text',
      label: '',
      required: false,
      options: []
    };
  
    function addField() {
      if (newField.name && newField.label) {
        fields.update(f => [...f, { ...newField, options: newField.options.filter(o => o.value && o.label) }]);
        newField = { name: '', type: 'text', label: '', required: false, options: [] };
      }
    }
  
    function removeField(index) {
      fields.update(f => f.filter((_, i) => i !== index));
    }
  
    function addOption() {
      newField.options = [...newField.options, { value: '', label: '' }];
    }
  
    function removeOption(index) {
      newField.options = newField.options.filter((_, i) => i !== index);
    }
  
    $: generatedCode = `
  <script>
    import SmartForm from './SmartForm.svelte';
  
    const fields = ${JSON.stringify($fields, null, 2)};
  
    function handleSubmit(event) {
      console.log('Form submitted:', event.detail);
    }
  <\/script>
  
  <SmartForm {fields} on:submit={handleSubmit} />
  
  ${$includeCSS ? `
  <style>
    /* Add your custom CSS here */
    .form-field {
      margin-bottom: 1rem;
    }
    label {
      display: block;
      margin-bottom: 0.5rem;
    }
    input, textarea, select {
      width: 100%;
      padding: 0.5rem;
      border: 1px solid #ccc;
      border-radius: 4px;
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
  ` : ''}`;
  
    function copyToClipboard() {
      navigator.clipboard.writeText(generatedCode);
      alert('Code copied to clipboard!');
    }
  </script>
  
  <div class="form-builder">
    <h2>Svelte Smart Form Builder</h2>
    
    <div class="form-config">
      <label>
        Form Name:
        <input type="text" bind:value={$formName}>
      </label>
      <label>
        <input type="checkbox" bind:checked={$includeCSS}>
        Include CSS
      </label>
    </div>
  
    <div class="field-adder">
      <h3>Add New Field</h3>
      <input type="text" bind:value={newField.name} placeholder="Field Name">
      <input type="text" bind:value={newField.label} placeholder="Field Label">
      <select bind:value={newField.type}>
        <option value="text">Text</option>
        <option value="email">Email</option>
        <option value="password">Password</option>
        <option value="number">Number</option>
        <option value="date">Date</option>
        <option value="checkbox">Checkbox</option>
        <option value="radio">Radio</option>
        <option value="select">Select</option>
        <option value="textarea">Textarea</option>
      </select>
      <label>
        <input type="checkbox" bind:checked={newField.required}>
        Required
      </label>
      
      {#if newField.type === 'radio' || newField.type === 'select'}
        <div class="options">
          <h4>Options</h4>
          {#each newField.options as option, i}
            <div class="option">
              <input type="text" bind:value={option.value} placeholder="Value">
              <input type="text" bind:value={option.label} placeholder="Label">
              <button on:click={() => removeOption(i)}>Remove</button>
            </div>
          {/each}
          <button on:click={addOption}>Add Option</button>
        </div>
      {/if}
      
      <button on:click={addField}>Add Field</button>
    </div>
  
    <div class="field-list">
      <h3>Current Fields</h3>
      {#each $fields as field, i}
        <div class="field">
          <span>{field.label} ({field.type})</span>
          <button on:click={() => removeField(i)}>Remove</button>
        </div>
      {/each}
    </div>
  
    <div class="code-output">
      <h3>Generated Code</h3>
      <pre>{generatedCode}</pre>
      <button on:click={copyToClipboard}>Copy Code</button>
    </div>
  </div>
  
  <style>
    .form-builder {
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
    }
    .form-config, .field-adder, .field-list, .code-output {
      margin-bottom: 20px;
    }
    .field, .option {
      display: flex;
      align-items: center;
      margin-bottom: 10px;
    }
    .field span, .option input {
      flex-grow: 1;
      margin-right: 10px;
    }
    pre {
      background-color: #f4f4f4;
      padding: 10px;
      border-radius: 4px;
      overflow-x: auto;
    }
  </style>