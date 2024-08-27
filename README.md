# Langtail Helm Chart
This repository contains Helm charts for deploying Langtail application on Kubernetes.

## Helm Chart

### Installation
```
helm repo add langtail https://langtail.github.com/langtail-k8s
helm repo update
helm install langtail langtail/langtail
```

### Upgrading
```
helm repo update
helm upgrade langtail langtail/langtail
```

### Configuration

TODO
- PRISMA_FIELD_ENCRYPTION_KEY: how to generate
- JWT_*: How to generate all of them

| Parameter                      | Description                                      | Default Value                                    |
|--------------------------------|--------------------------------------------------|--------------------------------------------------|
| `EVALUATOR_URL`                | URL for the Evaluator                            | `https://default-evaluator-url.com`              |
| `EVALUATOR_API_KEY`            | API key for the Evaluator                        | `default-evaluator-api-key`                      |
| `AUTH_URL`                     | URL for the authentication service               | `https://default-auth-url.com`                   |
| `AUTH_SECRET`                  | Authentication secret                            | `default-auth-secret`                            |
| `DATABASE_URL`                 | Database connection URL                          | `postgresql://user:password@localhost:5432/database` |
| `PRISMA_FIELD_ENCRYPTION_KEY`  | Encryption key for Prisma fields                 | `default-prisma-field-encryption-key`            |
| `JWT_PRIVATE`                  | JWT private key                                  | `default-jwt-private-key`                        |
| `JWT_PUBLIC`                   | JWT public key                                   | `default-jwt-public-key`                         |
| `JWT_SIGNING_KEY`              | JWT signing key                                  | `default-jwt-signing-key`                        |
| `LANGTAIL_MAGIC_TOKEN`         | Magic token for Langtail                         | `default-langtail-magic-token`                   |
| `LANGTAIL_MAGIC_TESTS_TOKEN`   | Magic tests token for Langtail                   | `default-langtail-magic-tests-token`             |
| `IMAGES_AWS_SECRET_ACCESS_KEY` | AWS secret access key for images                 | `default-aws-secret-access-key`                  |
| `SMTP_URL`                     | SMTP connection URL                              | `smtp://user:password@smtp.example.com:587`      |
| `EMAIL_VERIFICATION_SECRET`    | Secret for email verification                    | `default-email-verification-secret`              |
| `EMAIL_FROM`                   | Default email address                            | `default@example.com`                            |
| `SENTRY_ENABLED`               | Flag to enable Sentry                            | `true`                                          |
| `TINYBIRD_API_URL`             | TODO: REMOVE                                     | `https://default-tinybird-api-url.com`           |
| `CLERK_SECRET_KEY`             | TODO: REMOVE                                     | `default-clerk-secret-key`                       |
| `CANNY_JWT_KEY`                | TODO: REMOVE                                     | `default-canny-jwt-key`                          |
| `NEXT_PUBLIC_REWARDFUL_API_KEY`| TODO: REMOVE                                     | `default-rewardful-api-key`                      |
| `TINYBIRD_API_TOKEN`           | TODO: REMOVE                                     | `default-tinybird-api-token`                     |
| `TINYBIRD_API_KEY`             | TODO: REMOVE                                     | `default-tinybird-api-key`                       |
| `STRIPE_SECRET_KEY`            | TODO: REMOVE                                     | `default-stripe-secret-key`                      |
| `LOOPS_API_KEY`                | TODO: REMOVE                                     | `default-loops-api-key`                          |


### SSO
| Provider                       | Variables                      |                    
|--------------------------------|--------------------------------|
| Google                         | `GOOGLE_ID`<br>`GOOGLE_SECRET` |
| Github                         | `GITHUB_ID`<br>`GITHUB_SECRET` |