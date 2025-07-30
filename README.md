# Automatic Knowledge Source (KS) Update via StackSpot API

This repository contains a GitHub Actions workflow to automatically update a Knowledge Source (KS) in StackSpot from repository files, using StackSpot’s official APIs.

## What is a Knowledge Source (KS)?

A **Knowledge Source (KS)** is a knowledge repository used by StackSpot AI to provide answers, suggestions, and automations based on documents, code, manuals, and other files. Keeping the KS updated ensures that StackSpot’s artificial intelligence always uses the most recent information from your project.

## Purpose of this Workflow

This workflow automates the process of updating the KS whenever there are changes to specific files (for example, the `README.md`). It performs the following steps:

1. Obtains an authentication token (JWT) using the project credentials.
2. Requests a signed URL to upload the file to StackSpot storage.
3. Uploads the file (e.g., `README.md`) to the signed URL.
4. Requests the conversion of the file into knowledge objects, automatically updating the KS.

## How it Works

The workflow is triggered automatically on pushes to the `main` branch or manually via `workflow_dispatch`. It uses environment variables and GitHub secrets for authentication and KS identification.

## Main Required Variables/Secrets

- `CLIENT_REALM`: Client realm in StackSpot IDM.
- `CLIENT_ID`: Client ID for authentication.
- `CLIENT_KEY`: Client Secret for authentication.

These secrets must be configured in the repository’s **Secrets** on GitHub.

## Updating the KS Slug

If you want to update a different Knowledge Source (KS), you must change the KS slug in the workflow configuration. The KS slug uniquely identifies the Knowledge Source you wish to update in StackSpot. Make sure to replace the existing slug value with the slug of your target KS in the workflow file (for example, in the `target_id` field of the upload step).

> **Note:** The KS slug must match the one created in StackSpot. If you are unsure about the correct slug, check your StackSpot dashboard or contact your administrator.

## Example Execution

When you update the `README.md` file and push to the `main` branch, the workflow will run automatically, sending the new content to the configured KS.

## Workflow Structure

The main workflow file is located at `.github/workflows/atualizar-ks.yml` and follows the best practices recommended by StackSpot.

## Notes

- The KS must be previously created in StackSpot.
- The `split_strategy` can be adjusted according to your use case.
- The workflow can be adapted to update other files or multiple KS.

## References

- [StackSpot Official Documentation – Knowledge Source](https://docs.stackspot.com/)
- [StackSpot Data Integration API](https://docs.stackspot.com/)
