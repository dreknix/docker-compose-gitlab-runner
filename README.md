# Docker compose instance for GitLab runner

## Register GitLab runner

Since GitLab 16.0 the process how to register a GitLab runner has changed.

### Create runner

#### Via GitLab GUI

When creating a runner the place to create a runner depends on the type of
runner (instance, group, project).

* Group runner: `Build` -> `Runners` -> `New group runner`
* Project runner: `Settings` -> `CI/CD` -> `Runners` -> `New project runner`

Get the authentication token of the runner.

### Via GitLab API

First you need an API token for creating a runner:

```
https://gitlab.example.com/-/user_settings/personal_access_tokens?name=GitLab+runner+token&scopes=create_runner
```

Create the Python GitLab configuration (`.python-gitlab.yml`):

``` console
task gitlab:create-config -- <GITLAB_TOKEN>
```

Create a project runner for project 4711:

``` console
$ task gitlab:runner:create-project -- 4711 "GitLab runner test instance"
id: 911
token: glrt-XXXXXXXXXXXXXXXXXXXX
```

Use the token for registering the runner.

### Register runner

After a runner is created the authentication token can be used for registering
the runner.

``` console
task gitlab:runner:register -- glrt-XXXXXXXXXXXXXXXXXXXX
```

!!! todo

    Register runner with [template](
    https://docs.gitlab.com/runner/register/#register-with-a-configuration-template).

## License

[MIT](https://github.com/dreknix/docker-compose-gitlab-runner/blob/main/LICENSE)
