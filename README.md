# Install Azure CLI GitHub Action

This GitHub Action is designed to install the Azure CLI on a GitHub runner.

## Inputs

The action accepts two inputs:

- `creds`: Azure credentials in JSON format. This is not required.
- `allow-no-subscriptions`: A flag to allow the login to succeed even if the account has no subscriptions. This  defaults to 'false'.

## Steps

The action consists of two main steps:

1. **Install Azure CLI**: This step updates the package lists, installs necessary packages, sets up the Microsoft GPG keyring, adds the Azure CLI repository to the list of apt sources, and finally installs the Azure CLI and jq.

2. **Azure login**: This step logs into Azure using the provided credentials. It only runs if the 'creds' input is not empty.

## Usage

To use this action in a workflow, include it as a step:

```yaml
steps:
  - name: Install and login to Azure
    uses: enosix/ghac-install-azure@stable
    with:
      creds: |
        {
          "clientId": "${{ secrets.AZURE_AD_CLIENT_ID }}",
          "clientSecret": "${{ secrets.AZURE_AD_CLIENT_SECRET }}",
          "subscriptionId": "${{ secrets.AZURE_SUBSCRIPTION_ID }}",
          "tenantId": "${{ secrets.AZURE_AD_TENANT_ID }}",
          "resourceManagerEndpointUrl": "https://management.azure.com/"
        }
      allow-no-subscriptions: true
```

In this example, the action is used to install the Azure CLI and log in to Azure using the provided credentials. The 
`creds` input is a JSON object that contains the Azure AD client ID, client secret, subscription ID, tenant ID, and 
resource manager endpoint URL. The `allow-no-subscriptions` input is set to 'true' to allow the login to succeed even 
if the account has no subscriptions.

## Updating the action
To push an update, manually run the `Test and Tag` workflow. This will test the action and create a new release. 
