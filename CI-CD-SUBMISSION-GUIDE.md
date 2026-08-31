# Movie Picture Pipeline - CI/CD Submission

This project contains GitHub Actions CI/CD workflows for the React/TypeScript frontend
and Flask/Python backend.

## Workflows

- `.github/workflows/frontend-ci.yaml`
- `.github/workflows/backend-ci.yaml`
- `.github/workflows/frontend-cd.yaml`
- `.github/workflows/backend-cd.yaml`

CI runs on pull requests to `main` when the relevant application changes, and can also
be started manually with `workflow_dispatch`.

CD runs on pushes to `main` when the relevant application changes, and can also be
started manually.

## Required GitHub Secrets

Create these repository secrets before running CD:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION`
- `EKS_CLUSTER_NAME`
- `ECR_FRONTEND_REPOSITORY`
- `ECR_BACKEND_REPOSITORY`
- `ECR_FRONTEND_REPOSITORY_URL`
- `ECR_BACKEND_REPOSITORY_URL`
- `REACT_APP_MOVIE_API_URL`

Do not commit AWS credentials into the repository.

`ECR_*_REPOSITORY` should be the ECR repository name used by the Docker tag.
`ECR_*_REPOSITORY_URL` should be the full ECR repository URL.

## AWS / EKS setup

Use the supplied `setup/terraform` configuration if provided by the course:

```bash
cd setup/terraform
terraform init
terraform apply
```

Then configure access for the GitHub Actions IAM user as required by the course
instructions and run the supplied `setup/init.sh` script.

## Verification

After CD succeeds:

```bash
kubectl get pods
kubectl get services
```

For the backend, verify:

```bash
curl http://<backend-service-address>/movies
```

The expected API data contains:

- Top Gun: Maverick
- Sonic the Hedgehog
- A Quiet Place

Open the frontend service address and confirm that the movie list is displayed.

## Important

The ZIP does not contain AWS credentials. Live ECR/EKS deployment must be performed
using the user's AWS account and GitHub repository secrets.
