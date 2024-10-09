# Svelte Smart Form

Svelte Smart Form is a powerful, flexible, and easy-to-use form builder component for Svelte applications. It allows you to dynamically generate forms based on a configuration object, handling validation and submission with minimal effort.



## Features

- 🚀 Dynamic field generation
- ✅ Built-in validation
- 🎨 Custom validation support
- ⚡ Real-time error handling
- 💅 Flexible styling
- ♿ Accessibility-friendly
- 🔌 Easy integration with existing Svelte projects

## Usage

To use Svelte Smart Form in your project:

1. Copy the `SmartForm.svelte` component into your project's components directory.

2. Import and use the SmartForm component in your Svelte file:

```svelte
<script>
import SmartForm from './path/to/SmartForm.svelte';

const fields = [
  { name: 'username', type: 'text', label: 'Username', required: true },
  { name: 'email', type: 'email', label: 'Email', required: true },
  // Add more fields as needed
];

function handleSubmit(event) {
  console.log('Form submitted:', event.detail);
}
</script>

<SmartForm {fields} on:submit={handleSubmit} />
```

3. Customize your form by modifying the `fields` array.

4. Handle form submission in the `handleSubmit` function.

## Field Configuration

Each field in the `fields` array can have the following properties:

- `name` (required): The name of the field
- `type` (required): The type of input (e.g., 'text', 'email', 'password', 'checkbox', 'radio', 'select', 'textarea')
- `label` (required): The label for the field
- `required` (optional): Whether the field is required
- `options` (required for 'radio' and 'select'): An array of options for radio buttons or select dropdowns
- `validate` (optional): A custom validation function
- `minLength` (optional): Minimum length for text inputs
- `maxLength` (optional): Maximum length for text inputs
- `pattern` (optional): A regex pattern for validation

## Form Builder

Svelte Smart Form also includes a Form Builder component that allows you to create forms visually and generate the corresponding code:

1. Copy the `SmartFormBuilder.svelte` component into your project's components directory.

2. Import and use the SmartFormBuilder component in your Svelte file:

```svelte
<script>
import SmartFormBuilder from './path/to/SmartFormBuilder.svelte';
</script>

<SmartFormBuilder />
```

## Styling

Svelte Smart Form comes with basic styling out of the box. You can easily customize the appearance by overriding the CSS classes in your Svelte component.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## Support

If you encounter any problems or have any questions, please open an issue on the GitHub repository.

## Acknowledgements

- [Svelte](https://svelte.dev/)
- [SvelteKit](https://kit.svelte.dev/)
- All contributors who have helped shape Svelte Smart Form

---

Made with ❤️ by Leon Kalema