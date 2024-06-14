
# Azure DevOps Pipeline Templates

This repository contains a collection of YAML templates for Azure DevOps pipelines to streamline CI/CD processes.

## Table of Contents

- [Description](#description)
- [Installation](#installation)
- [Usage](#usage)
  - [Sample Pipeline: Build and Deploy .NET Application](#sample-pipeline-build-and-deploy-net-application)
- [Templates](#templates)
- [Contributing](#contributing)
- [License](#license)

## Description

The Azure DevOps Pipeline Templates project aims to provide reusable YAML templates to simplify and standardize CI/CD pipelines in Azure DevOps.

## Installation

To get started, clone the repository.

```bash
git clone https://github.com/wesellis/Azure-DevOps-Pipeline-Templates.git
cd Azure-DevOps-Pipeline-Templates
```

## Usage

### Sample Pipeline: Build and Deploy .NET Application

To use the build and deploy .NET application pipeline, include the `dotnet-build-deploy.yml` template in your Azure DevOps pipeline.

```yaml
# azure-pipelines.yml
trigger:
- main

extends:
  template: templates/dotnet-build-deploy.yml
  parameters:
    project: '**/*.csproj'
    buildConfiguration: 'Release'
    azureSubscription: 'AzureServiceConnection'
    appServiceName: 'YourAppServiceName'
    resourceGroupName: 'YourResourceGroupName'
```

### Other Templates

- **dotnet-build-deploy.yml**: Template to build and deploy a .NET application.
- **node-build-deploy.yml**: Template to build and deploy a Node.js application.
- **python-build-deploy.yml**: Template to build and deploy a Python application.
- **docker-build-push.yml**: Template to build and push a Docker image.
- **terraform-init-apply.yml**: Template to initialize and apply Terraform configurations.
- **arm-deploy.yml**: Template to deploy Azure Resource Manager templates.
- **k8s-deploy.yml**: Template to deploy to a Kubernetes cluster.

## Contributing

We welcome contributions to improve and expand this collection of pipeline templates. Please see our [CONTRIBUTING.md](CONTRIBUTING.md) file for guidelines.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
