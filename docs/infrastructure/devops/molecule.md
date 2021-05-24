# Molecule

Molecule <badge-stars repo='ansible-community/molecule'></badge-stars>
<badge-doc href='https://molecule.readthedocs.io'></badge-doc>  is designed to
aid in the development and testing of Ansible roles. It provides support for:

- testing with multiple instances, operating systems and distributions;
- virtualization providers;
- test frameworks and testing scenarios.


## Installation

With [pipx]:

```terminal
pipx install ansible
pipx inject --include-apps ansible 'molecule[docker]'
```

## Role initialisation

New role are initialized with the `molecule init role` command. Configuration
can contain [environment
variables](https://molecule.readthedocs.io/en/latest/configuration.html) and is
beeing loaded from:

- project config
- local config (~/.config/molecule/config.yml)
- default config (molecule.yml)

Options can be set on the command line

```terminal
Usage: molecule init role [OPTIONS] ROLE_NAME

  Initialize a new role for use with Molecule.

Options:
  --dependency-name [galaxy]      Name of dependency to initialize. (galaxy)
  -d, --driver-name [delegated|docker]
                                  Name of driver to initialize. (delegated)
  --lint-name [yamllint]          Name of lint to initialize. (yamllint)
  --provisioner-name [ansible]    Name of provisioner to initialize. (ansible)
  --verifier-name [ansible|testinfra]
                                  Name of verifier to initialize. (ansible)
  --help                          Show this message and exit.
```

Note: default [configuration](https://molecule.readthedocs.io/en/latest/configuration.html) is defined in [`molecule.config`](https://github.com/ansible-community/molecule/blob/master/molecule/config.py)





## Scenarios

Scenarios can be though as multiple test suites. Each scenario is configured in `molecule.yml` with top level key:

- `dependency`: dependency manager [galaxy, gilt, shell]
- `driver`: driver for spinning-up the environment to test on [delegated, docker, podman]
- `lint`: external lint commands.
- `platforms`: instances to be tested, and the groups to which the instances belong.
- `provisioner`: handles provisioning and converging the role (ansible).
- `scenario`: scenarios are first-class citizens with a top-level configuration syntax. It is a self-contained directory containing everything necessary for testing the role in a particular way. The default scenario is named default, and every role should contain a default scenario.
- `state`: internal bookkeeping mechanism
- `verifier`: test suite


## Action

- dependency
- check
- converge
- cleanup
- create
- destroy
- prepare
- idempotence
- verify

Default scenarios sequences are:

- "check_sequence": [ "dependency", "cleanup", "destroy", "create", "prepare", "converge", "check", "cleanup", "destroy", ],
- "cleanup_sequence": ["cleanup"],
- "converge_sequence": ["dependency", "create", "prepare", "converge"],
- "create_sequence": ["dependency", "create", "prepare"],
- "destroy_sequence": ["dependency", "cleanup", "destroy"],
- "test_sequence": [ "dependency", "lint", "cleanup", "destroy", "syntax", "create", "prepare", "converge", "idempotence", "side_effect", "verify", "cleanup", "destroy",

The corresponding playbooks are stored in the files whose default names are:

- "cleanup": "cleanup.yml",
- "create": "create.yml",
- "converge": "converge.yml",
- "destroy": "destroy.yml",
- "prepare": "prepare.yml",
- "side_effect": "side_effect.yml",
- "verify": "verify.yml",


## Creating a new role

```console
molecule init role my-new-role
```

or add to an existing role:

```console
molecule scenario role my-new-role
```

## Role metadata

 <badge-doc href='https://galaxy.ansible.com/docs/contributing/creating_role.html' logo="ansible"></badge-doc>


!!! danger "Role name `role_name`"

    In the past, Galaxy would apply a regex expression to the GitHub repository
    name and automatically remove ‘ansible-‘ and ‘ansible-role-‘. For example,
    if your repository name was ‘ansible-role-apache’, the role name would
    translate to ‘apache’. Galaxy no longer does this automatically. Instead,
    use the role_name setting to tell Galaxy what the role name should be.


## Links

- [ Jeff Geerling's blog ](https://www.jeffgeerling.com/blog/2018/testing-your-ansible-roles-molecule)
- [Fabian von Feilitzsch - Practical Ansible Testing with Molecule](https://www.ansible.com/hubfs//AnsibleFest%20ATL%20Slide%20Decks/Practical%20Ansible%20Testing%20with%20Molecule.pdf)

# FAQ

[ERROR! no action detected in task](https://stackoverflow.com/questions/47159193/why-does-ansible-show-error-no-action-detected-in-task-error)


[pipx]: https://pipxproject.github.io/pipx
