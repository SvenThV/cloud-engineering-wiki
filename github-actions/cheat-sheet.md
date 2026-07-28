| Concept           | Remember                                   |
| ----------------- | ------------------------------------------ |
| Workflow          | YAML file                                  |
| Job               | Own runner                                 |
| Step              | Single task                                |
| Runner            | Fresh VM                                   |
| uses              | Execute an Action                          |
| run               | Execute shell commands                     |
| with              | Pass parameters                            |
| needs             | Connect jobs                               |
| env               | Non-sensitive variables                    |
| secrets           | Sensitive values                           |
| expressions       | `${{ }}`                                   |
| checkout          | Download repository                        |
| setup-terraform   | Install Terraform                          |
| azure/login       | Authenticate to Azure                      |
| artifacts         | Share files between jobs                   |
| cache             | Speed up workflows                         |
| working-directory | Execute commands in a subdirectory         |
| workflow_dispatch | Manual execution                           |
| push              | Trigger on push                            |
| pull_request      | Trigger on PR                              |
| schedule          | Cron execution                             |
| OIDC              | Azure authentication without client secret |
