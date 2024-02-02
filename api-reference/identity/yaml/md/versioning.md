[//]: # (# Versions)

[//]: # ()
[//]: # (| Version | Date       | Person     | Company | Summary of changes                       |)

[//]: # (|---------|------------| ---------- | ------- |------------------------------------------|)

[//]: # (| 0.1.0   | 18-04-2023 | Jon Sharpe | Fondy   | Release of first draft.                  |)

[//]: # (| 2.0.0   | 10-08-2023 | Jon Sharpe | Fondy   | Release of final version for Client User |)

[//]: # (| 2.1.0   | 24-10-2023 | Jon Sharpe | Fondy   | Release of the Compliance Profile        |)

[//]: # ()
[//]: # (# Supported Endpoints in versions)

[//]: # ()
[//]: # (### NOTES)

[//]: # ()
[//]: # (This call is for the account visible to your user that you are using, If you use multiple users, this list could be different the URL is `.../api/v1/{clientRef}/...` where the client ref is YOUR specific client `UUID` that is provided by Fondy upon successful onboarding.)

[//]: # ()
[//]: # (## Endpoints support)

[//]: # ()
[//]: # (Route endpoint ->  /{client id}/onboarding)

[//]: # ()
[//]: # (| API endpoint                               | Method | Support in Version | Description                          |)

[//]: # (|--------------------------------------------|--------|--------------------|--------------------------------------|)

[//]: # (| `/identity`                                | `GET`  | 1.0                | Get all identities                   |)

[//]: # (| `/identity`                                | `POST` | 1.0                | create an identity                   | )

[//]: # (| `/identity/{id}`                           | `GET`  | 1.0                | Get specific identity                |)

[//]: # (| `/onboarding/compliace/profile`            | `POST` | 2.1.0              | Create a specific compliance profile |)

[//]: # (| `/onboarding/compliace/profile/{id}`       | `GET`  | 2.1.0              | Get specific compliance              |)
