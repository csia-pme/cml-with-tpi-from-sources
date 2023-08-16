# CML with Terraform Provider Iterative (TPI) from sources

This repository demonstrates the usage of CML with Terraform Provider Iterative
from sources.

## Configuration

The following elements were required to configure CML to use TPI from sources:

1. Create a personal access token (PAT) to the repository. The PAT must have the
`repo` scope
2. Create a new
[repository secret](https://github.com/csia-pme/cml-with-tpi-from-sources/settings/secrets/actions)
under the name `CML_PAT` with the value of the generated PAT. It is used in the
[`.github/workflows/workflow.yml`](.github/workflows/workflow.yml) file.
3. Create a new
[repository secret](https://github.com/csia-pme/cml-with-tpi-from-sources/settings/secrets/actions)
under the name `GCP_SERVICE_ACCOUNT_KEY` with the value of the Google Service
Account Key. It is used in the
[`.github/workflows/workflow.yml`](.github/workflows/workflow.yml) file. It can
be generated with the following command:
    ```sh
    # Export the Google Cloud Platform (GCP) Project ID
    export GCP_PROJECT_ID=<GCP_PROJECT_ID>

    # Create the Google Service Account
    gcloud iam service-accounts create gcp-service-account \
        --display-name="GCP Service Account"

    # Set the Kubernetes Cluster permissions for the Google Service Account
    gcloud projects add-iam-policy-binding $GCP_PROJECT_ID \
        --member="serviceAccount:gcp-service-account@${GCP_PROJECT_ID}.iam.gserviceaccount.com" \
        --role="roles/container.admin"

    # Create the Google Service Account Key
    gcloud iam service-accounts keys create ~/.config/gcloud/google-service-account-key.json \
        --iam-account=gcp-service-account@${GCP_PROJECT_ID}.iam.gserviceaccount.com

    # Display the Google Service Account Key
    cat ~/.config/gcloud/google-service-account-key.json
    ```
