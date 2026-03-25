# Kleff Plugin Registry

Welcome to the official [Kleff](https://github.com/kleffio/platform) Plugin Registry! 

This repository acts as the central catalog for discovering, sharing, and distributing plugins for the Kleff platform. It contains a single index file, `plugins.json`, which the Kleff core platform fetches dynamically to populate the in-app marketplace.

## 🚀 Submitting a Plugin

Have you built a custom authentication provider, a billing integration, or a new game server adapter? We'd love to add it to the registry so other users can install it seamlessly!

To publish your plugin to the Kleff community, follow these simple steps:

1. **Host your plugin code**: Create a public repository (e.g., GitHub, GitLab) containing your plugin's Go code, `kleff-plugin.json` manifest, and Dockerfile.
2. **Publish your plugin image**: Build and publish your Docker container image to a public container registry (e.g., Docker Hub, GitHub Container Registry).
3. **Fork this repository**.
4. **Update `plugins.json`**: Append your plugin's metadata object to the end of the JSON array.
5. **Open a Pull Request**: Submit your changes to us for review. Once approved and merged, your plugin will immediately become available in the Kleff Panel for all users!

## 📄 Manifest Structure

When appending your plugin to `plugins.json`, please use the following structure. This strictly mirrors the `CatalogManifest` struct expected by the Kleff core engine.

```json
{
  "id": "my-custom-plugin",
  "name": "My Custom Plugin",
  "type": "idp", 
  "description": "A short, one-sentence description of what your plugin does.",
  "longDescription": "## Setup Guide\n\nMarkdown-formatted detailed description and step-by-step setup instructions.",
  "tags": ["sso", "community", "open-source"],
  "author": "Your Name or Organization",
  "repo": "https://github.com/your-username/my-custom-plugin",
  "docs": "https://your-domain.com/docs/plugin-guide",
  "image": "ghcr.io/your-username/my-custom-plugin",
  "version": "1.0.0",
  "minKleffVersion": "0.5.0",
  "license": "MIT",
  "verified": false,
  "config": [
    {
      "key": "API_TOKEN",
      "label": "API Token",
      "description": "Your access token for the external service.",
      "type": "secret",
      "required": true
    }
  ]
}
```

### Configuration Fields

The `config` array tells the Kleff panel exactly what environment variables your plugin requires to function. Kleff will automatically generate a dynamic installation UI based on these fields, securely store the values provided by the admin, and inject them into your plugin's container runtime.

Supported `type` values:
- `string`: Standard text input.
- `secret`: Password/Masked input (values are encrypted at rest).
- `number`: Numeric input.
- `boolean`: Checkbox / Toggle.
- `url`: Validated URL input.
- `select`: Dropdown menu (requires an additional `options` array).

## 🛡️ "Verified" Plugins

You may notice some plugins have `"verified": true`. This badge is reserved for official integrations maintained directly by the core Kleff team, or trusted partners that undergo rigorous security and performance audits. 

All standard community submissions should initially set this to `false`.
