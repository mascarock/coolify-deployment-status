# Coolify Deployment Notification Workflow

This repository contains a GitHub Actions workflow for automating the deployment of applications using Coolify. The workflow ensures deployments are tracked and updates the GitHub commit status depending on the deployment outcome.

## How Does It Work?

1. **Trigger**: The workflow is triggered when there is a push to the `staging` branch.
2. **Set Deployment Status**: The deployment status is set to "pending" at the start of the process to indicate that deployment is in progress.
3. **Monitor Coolify Deployment**: It monitors the deployment status by polling the Coolify API until a final state (success or failure) is determined.
4. **Update Deployment Status**: Based on the final result, it updates the GitHub commit status to either "success" or "failure".

The workflow script utilizes several environment variables that are set as GitHub secrets for security purposes. It interacts with both GitHub's and Coolify's APIs to manage deployment status and provide visibility on the state of the deployment.

## GitHub Secrets Explained
Below is a list of the GitHub secrets required for the workflow to function:

| Secret Name            | Description                                                                                             |
|------------------------|---------------------------------------------------------------------------------------------------------|
| `GITHUB_PAT`           | Personal Access Token for GitHub. Used to authenticate and set deployment statuses via GitHub API.     |
| `COOLIFY_AUTH_TOKEN`   | Authorization token for Coolify’s API. Enables access to Coolify’s deployment and application statuses.|
| `COOLIFY_BASE_URL`     | Base URL for Coolify’s API endpoint. Used to construct API requests for retrieving deployment data.    |
| `COOLIFY_APP_ID`       | The unique application ID in Coolify for the staging environment. Used to fetch status and monitor deployments.|

## Requirements
- **GitHub Secrets**: You need to set up the above GitHub secrets in your repository settings to run this workflow successfully.
- **Coolify Setup**: Ensure that Coolify is properly configured and your app's `APP_ID` and `AUTH_TOKEN` are accessible.
- **jq**: This workflow uses `jq` to parse JSON responses. Make sure it is available in your GitHub runner environment.

## Example Usage

For an in-depth explanation of this workflow, you can also refer to the related article on my website: [Coolify Deployment Notification Workflow](https://mascaro.eu/automating-coolify-deployments-github-actions).
To use this workflow, add the `notify_deployment.yml` file to the `.github/workflows` directory of your repository. Make sure to configure the necessary GitHub secrets mentioned above.

For more details on Coolify and its deployment automation capabilities, you can refer to the [Coolify Documentation](https://coolify.io/docs/).
