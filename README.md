# Langtail Helm Chart

This repository contains Helm charts for deploying the Langtail application on Kubernetes.

© 2024 Langtail. All rights reserved.

This project is available only under a commercial license from Langtail. 
Unauthorized copying, modification, distribution, or use of this software is strictly prohibited.

To obtain a license or discuss commercial usage, please contact:
hi@langtail.com

## Helm Chart

### Installation

To install the Langtail Helm chart:

```bash
helm repo add langtail https://langtail.github.com/langtail-k8s
helm repo update
helm install langtail langtail/langtail
```

### Upgrading

To upgrade an existing deployment:

```bash
helm repo update
helm upgrade langtail langtail/langtail
```

#### Upgrade Process

The upgrade process in the Langtail Helm chart includes **Helm hooks** that ensure database migrations are applied **before** the new version of the application is deployed. This means:

- A **migration job** is triggered as part of the Helm upgrade process.
- The job ensures that any necessary database changes are made prior to spinning up the new version of the application.
- This mechanism ensures smooth transitions between versions and avoids potential database compatibility issues.

You don't need to run migrations manually — the Helm hooks handle this automatically during each upgrade.

### Configuration

Below is a list of all available configuration parameters that can be set during installation or upgrade.

#### Secrets and Key Generation

- **AUTH_SECRET**: To generate a secure authentication secret, run:
  ```bash
  openssl rand -base64 32
  ```

- **JWT_PRIVATE** and **JWT_PUBLIC**: These are required for signing and verifying JWTs. You can generate them using [https://mkjwk.org/](https://mkjwk.org/):
  - Select **EC** as the key type.
  - Use **P-256** as the curve.

- **JWT_SIGNING_KEY**: You can generate the JWT signing key using the same tool:
  - Select **oct** as the key type.
  - Use **Signature** for the key usage.

- **PRISMA_FIELD_ENCRYPTION_KEY**: This key is used to encrypt fields in Prisma. Generate it with the following command:
  ```bash
  openssl rand -base64 32
  ```

| Parameter                      | Description                                      | Default Value                                    |
|--------------------------------|--------------------------------------------------|--------------------------------------------------|
| `SMTP_URL`                     | SMTP connection URL                              | `smtp://user:password@smtp.example.com:587`      |
| `EMAIL_FROM`                   | Default email address                            | `default@example.com`                            |
| `EMAIL_VERIFICATION_SECRET`    | Secret for email verification **Must be generated**                    | `default-email-verification-secret`              |
| `JWT_PRIVATE`                  | JWT private key. **Must be generated**.          | `default-jwt-private-key`                        |
| `JWT_PUBLIC`                   | JWT public key. **Must be generated**.           | `default-jwt-public-key`                         |
| `JWT_SIGNING_KEY`              | JWT signing key. **Must be generated**.          | `default-jwt-signing-key`                        |
| `AUTH_URL`                     | URL for the authentication service               | `https://default-auth-url.com`                   |
| `AUTH_SECRET`                  | Authentication secret. **Must be generated**.    | `default-auth-secret`                            |
| `DATABASE_URL`                 | Database connection URL                          | `mysql://user:password@localhost:5432/database` |
| `MIGRATIONS_DATABASE_URL`      | Database connection URL for migrations. Can be the same as DATABASE_URL, but in case you want to use a different user to apply migrations, there's a way | `mysql://user:password@localhost:5432/database` |
| `PRISMA_FIELD_ENCRYPTION_KEY`  | Encryption key for Prisma fields. **Must be generated**. | `default-prisma-field-encryption-key`            |
| `IMAGES_AWS_SECRET_ACCESS_KEY` | AWS secret access key for images                 | `default-aws-secret-access-key`                  |
| `SENTRY_ENABLED`               | Flag to enable Sentry                            | `true`                                           |
| `GOOGLE_ID`                    | Google OAuth client ID                           | `default-google-id`                              |
| `GOOGLE_SECRET`                | Google OAuth client secret                       | `default-google-secret`                          |
| `GITHUB_ID`                    | GitHub OAuth client ID                           | `default-github-id`                              |
| `GITHUB_SECRET`                | GitHub OAuth client secret                       | `default-github-secret`                          |

### SSO Configuration

To configure single sign-on (SSO) for Google and GitHub, set the following environment variables:

| Provider                       | Variables                      |                    
|--------------------------------|--------------------------------|
| **Google**                     | `GOOGLE_ID`<br>`GOOGLE_SECRET` |
| **GitHub**                     | `GITHUB_ID`<br>`GITHUB_SECRET` |

For instructions on generating OAuth credentials, refer to:

- [Google Provider Documentation](https://next-auth.js.org/providers/google)
- [GitHub Provider Documentation](https://next-auth.js.org/providers/github)

### Adding Extra Manifests
The Helm chart includes an `extraManifests` field in values.yaml, which allows you to inject additional Kubernetes resources into your deployment. This is useful for adding custom resources like ConfigMaps, Secrets, or any other Kubernetes manifests that are not included in the default chart.
