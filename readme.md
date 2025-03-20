# Dokploy Deployment GitHub Action

This GitHub Action triggers a deployment on Dokploy.

## Inputs

### `api_key`

**Required** The Dokploy API key. You can create one from `<YOUR DOKPLOY URL>/dashboard/settings/profile`.

### `application_id`

**Required** The Dokploy application ID. `<YOUR DOKPLOY URL>/dashboard/project/osLZ6EdGJu8u_IEBcUnGv/services/application/<APPLICATION_ID>`

### `dokploy_url`

**Required** Dokploy dashboard URL (this should have the Dokploy API accessible at /api) - no trailing backslash.

e.g. `https://dokploy.example.com`


### `service_type`

**Optional** Type of Dokploy service (`compose` or `application`)

**Default** `application`

### `deploy`

**Optional** When set to false, deployment isn't triggered. 

**Default** true

### `secrets`

**Optional** Pass `${{ toJSON(secrets) }}` to set environment variables from GitHub secrets.

**Default** null

### `vars`

**Optional** Pass `${{ toJSON(vars) }}` to set environment variables from GitHub variables.

**Default** null

## Usage

To use this action, include it in your workflow file as follows:

```yaml
name: Deploy on Dokploy

on: [push]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Dokploy Deployment
      uses: vicke4/dokploy-deploy-with-secrets@v0.1.2
      with:
        api_key: ${{ secrets.DOKPLOY_API_KEY }}
        application_id: ${{ secrets.DOKPLOY_APPLICATION_ID }}
        dokploy_url: ${{ secrets.DOKPLOY_URL }}
        secrets: ${{ toJSON(secrets) }}
        vars: ${{ toJSON(vars) }}
```

## Contributing

Contributions are welcome! Please feel free to submit a pull request or open an issue for any bugs or feature requests.


## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
