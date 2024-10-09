<script>
    import SmartForm from '$lib/SmartForm.svelte';
    import SmartFormBuilder from '$lib/SmartFormBuilder.svelte';
    
    const fields = [
        { name: 'name', type: 'text', label: 'Name', required: true },
        { name: 'email', type: 'email', label: 'Email', required: true },
        { name: 'password', type: 'password', label: 'Password', required: true, minLength: 8 },
        { name: 'birthdate', type: 'date', label: 'Birth Date', required: true },
        { name: 'phone', type: 'tel', label: 'Phone', pattern: '^[0-9]{10}$', validate: (value) => value.startsWith('0') ? 'Phone number should not start with 0' : '' },
        { name: 'subscribe', type: 'checkbox', label: 'Subscribe to newsletter' },
        { name: 'gender', type: 'radio', label: 'Gender', required: true, options: [
            { value: 'male', label: 'Male' },
            { value: 'female', label: 'Female' },
            { value: 'other', label: 'Other' }
        ]},
        { name: 'country', type: 'select', label: 'Country', required: true, options: [
            { value: 'sv', label: 'Sweden' },
            { value: 'ug', label: 'Uganda' },
            { value: 'uk', label: 'United Kingdom' }
        ]},
        { name: 'message', type: 'textarea', label: 'Message', required: true, minLength: 10 }
    ];
    
    function handleSubmit(event) {
        console.log('Form submitted:', event.detail);
    }
</script>

<svelte:head>
    <title>Svelte Smart Form - Dynamic Form Builder for Svelte Applications</title>
    <meta name="description" content="Create dynamic, validated forms easily with Svelte Smart Form. Try our live demo and form builder to generate custom forms for your Svelte projects.">
    <meta name="keywords" content="Svelte, form builder, dynamic forms, form validation, Svelte components">
</svelte:head>

<header>
    <h1>Svelte Smart Form</h1>
    <p>Dynamic Form Builder for Svelte Applications</p>
</header>

<nav>
    <a href="#about">About</a>
    <a href="#demo">Live Demo</a>
    <a href="#builder">Form Builder</a>
    <a href="#how-to-use">How to Use</a>
</nav>

<main>
    <section id="about">
        <h2>About Svelte Smart Form</h2>
        <p>Svelte Smart Form is a powerful and flexible form component that dynamically generates form fields based on a configuration object. It simplifies form creation and handling in Svelte applications, saving you time and effort.</p>
        
        <h3>Key Features</h3>
        <ul>
            <li>Dynamic Field Generation</li>
            <li>Built-in Validation</li>
            <li>Custom Validation</li>
            <li>Real-time Error Handling</li>
            <li>Flexible Styling</li>
            <li>Accessibility</li>
            <li>Easy Integration</li>
        </ul>
        
        <a href="#demo" class="cta-button">Try Live Demo</a>
    </section>

    <section id="demo">
        <h2>Live Demo</h2>
        <p>Experience the power of Svelte Smart Form with this registration form example. It includes various field types and demonstrates built-in and custom validation.</p>
        
        <SmartForm {fields} on:submit={handleSubmit} />
        
        <p>
            <strong>Note:</strong> This is a demo form. No data is actually submitted.
        </p>
    </section>

    <section id="builder">
        <h2>Form Builder</h2>
        <p>Create your own custom form using our interactive Form Builder. Design your form structure, then copy the generated code to use in your Svelte project.</p>
        
        <SmartFormBuilder />
    </section>

    <section id="how-to-use">
        <h2>How to Use Svelte Smart Form</h2>
        <ol>
            <li><strong>Install:</strong> Add the SmartForm component to your Svelte project.</li>
            <li><strong>Design:</strong> Use the Form Builder above to design your form structure.</li>
            <li><strong>Copy:</strong> Copy the generated code from the Form Builder.</li>
            <li><strong>Paste:</strong> Create a new .svelte file in your project and paste the copied code.</li>
            <li><strong>Import:</strong> Import your new form component wherever you need it in your Svelte app.</li>
            <li><strong>Enjoy:</strong> Your form will handle validation and submission based on your configuration!</li>
        </ol>
        
        <p>For more detailed instructions, check out our <a href="#">documentation</a>.</p>
    </section>
</main>

<footer>
    <p>Svelte Smart Form &copy; 2024 | <a href="https://kit.svelte.dev">Learn more about Svelte</a></p>
</footer>

<style>
    :global(body) {
        font-family: Arial, sans-serif;
        line-height: 1.6;
        color: #333;
        max-width: 1200px;
        margin: 0 auto;
        padding: 20px;
    }
    header {
        background-color: #4CAF50;
        color: white;
        text-align: center;
        padding: 1rem;
        margin-bottom: 2rem;
    }
    nav {
        display: flex;
        justify-content: center;
        margin-bottom: 2rem;
    }
    nav a {
        margin: 0 1rem;
        color: #4CAF50;
        text-decoration: none;
    }
    section {
        margin-bottom: 3rem;
    }
    h1, h2, h3 {
        color: #4CAF50;
    }
    .cta-button {
        display: inline-block;
        background-color: #4CAF50;
        color: white;
        padding: 0.5rem 1rem;
        text-decoration: none;
        border-radius: 4px;
        margin-top: 1rem;
    }
    footer {
        background-color: #f4f4f4;
        text-align: center;
        padding: 1rem;
        margin-top: 2rem;
    }
</style>