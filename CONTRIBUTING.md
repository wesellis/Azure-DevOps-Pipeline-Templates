# Contributing to Azure DevOps Pipeline Templates

We welcome contributions to this repository! This document provides guidelines for contributing.

## How to Contribute

### 1. Fork the Repository
- Fork this repository to your GitHub account
- Clone your fork locally
- Create a new branch for your changes

### 2. Make Your Changes
- Add new pipeline templates or improve existing ones
- Follow the established naming conventions
- Include comprehensive parameter documentation
- Test your templates thoroughly

### 3. Template Standards

#### Naming Convention
- Use descriptive names: `technology-action-target.yml`
- Examples: `dotnet-build-deploy.yml`, `docker-build-push.yml`

#### Parameter Guidelines
- Include parameter descriptions and default values
- Use appropriate parameter types (string, boolean, object, etc.)
- Group related parameters logically
- Provide examples in comments

#### Template Structure
```yaml
# Template Description
# Brief explanation of what this template does

parameters:
- name: parameterName
  type: string
  default: 'defaultValue'
  displayName: 'Human-readable name'

stages:
- stage: StageName
  displayName: 'Stage Display Name'
  jobs:
  - job: JobName
    # Job implementation
```

#### Best Practices
- Use meaningful display names for all tasks
- Include error handling where appropriate
- Add conditional logic for optional features
- Use output variables for data sharing between stages
- Include comprehensive logging

### 4. Documentation Requirements

#### Template Documentation
Each template should include:
- Clear description of purpose
- Complete parameter list with descriptions
- Usage examples
- Prerequisites and requirements
- Known limitations

#### README Updates
When adding new templates:
- Update the main README.md
- Add template to the list with description
- Include usage example
- Update table of contents if needed

### 5. Testing Guidelines

#### Template Validation
- Validate YAML syntax
- Test with different parameter combinations
- Verify all conditional paths work
- Test error scenarios

#### Integration Testing
- Test templates in actual Azure DevOps pipelines
- Verify with different Azure service connections
- Test with various project types and configurations

### 6. Submission Process

#### Pull Request Requirements
- Clear, descriptive title
- Detailed description of changes
- Link to any related issues
- Include testing performed
- Update documentation as needed

#### Pull Request Template
```markdown
## Description
Brief description of changes

## Type of Change
- [ ] New template
- [ ] Template improvement
- [ ] Bug fix
- [ ] Documentation update
- [ ] Breaking change

## Testing Performed
- [ ] YAML syntax validation
- [ ] Template testing in Azure DevOps
- [ ] Parameter validation
- [ ] Error scenario testing

## Checklist
- [ ] Code follows established conventions
- [ ] Self-review completed
- [ ] Documentation updated
- [ ] Testing completed
- [ ] No breaking changes (or clearly documented)
```

### 7. Template Categories

#### Build Templates
- Language-specific build processes
- Dependency management
- Testing and code coverage
- Artifact creation

#### Deploy Templates
- Application deployment
- Infrastructure provisioning
- Database updates
- Configuration management

#### Infrastructure Templates
- ARM/Bicep deployments
- Terraform workflows
- Kubernetes deployments
- Container operations

#### Quality Templates
- Code analysis
- Security scanning
- Performance testing
- Compliance checks

### 8. Review Process

#### Automated Checks
- YAML syntax validation
- Template parameter validation
- Documentation completeness check
- Naming convention verification

#### Manual Review
- Code quality assessment
- Security best practices review
- Template effectiveness evaluation
- Documentation review

### 9. Community Guidelines

#### Communication
- Be respectful and constructive
- Provide clear explanations
- Help others learn and improve
- Share knowledge and best practices

#### Issue Reporting
- Use issue templates when available
- Provide clear reproduction steps
- Include relevant environment details
- Tag issues appropriately

### 10. Getting Help

#### Resources
- [Azure DevOps YAML Schema Reference](https://docs.microsoft.com/azure/devops/pipelines/yaml-schema)
- [Pipeline Templates Documentation](https://docs.microsoft.com/azure/devops/pipelines/process/templates)
- [Azure DevOps Tasks Reference](https://docs.microsoft.com/azure/devops/pipelines/tasks)

#### Support
- Create an issue for bugs or feature requests
- Start a discussion for questions or ideas
- Tag maintainers for urgent issues

## Recognition

Contributors will be recognized in:
- Repository contributors list
- Release notes for significant contributions
- Special mentions for innovative templates

Thank you for contributing to make Azure DevOps pipelines better for everyone!
