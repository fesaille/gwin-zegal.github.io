# Jupyter

## Introduction

<badge-doc href='https://jupyter.org/documentation'></badge-doc>



**Jupyter Core** <badge-stars repo='jupyter/jupyter_core'></badge-stars> <badge-doc href='https://jupyter-core.readthedocs.io/'></badge-doc> contains base application classes and configuration inherited by other projects. The `jupyter` root command is defined [here](https://github.com/jupyter/jupyter_core/blob/master/jupyter_core/command.py).

**Jupyter Client** <badge-stars repo='jupyter/jupyter_client'></badge-stars> <badge-doc href='https://jupyter-client.readthedocs.io'></badge-doc> provides the Python API for starting, managing and communicating with Jupyter kernels

**Jupyter Server** <badge-stars repo='jupyter/jupyter_server'></badge-stars> <badge-doc href='https://jupyter-server.readthedocs.io'></badge-doc> provides the backend (i.e. the core services, APIs, and REST endpoints) for Jupyter web applications like Jupyter notebook, JupyterLab, and Voila.

**Jupyterlab Server** <badge-stars repo='jupyterlab/jupyterlab_server'></badge-stars> 

**IPykernel** <badge-stars repo='ipython/ipykernel'></badge-stars> <badge-doc href='https://ipython.readthedocs.io'></badge-doc>


### Traitlets

Traitlets  <badge-stars repo='ipython/traitlets'></badge-stars> <badge-doc href='https://traitlets.readthedocs.io'></badge-doc>  is a framework that lets Python classes have **attributes** with **type checking**, dynamically calculated default values, and ‘on change’ callbacks (*observer* pattern <badge-doc href='https://en.wikipedia.org/wiki/Observer_pattern' logo='Wikipedia' label=''></badge-doc> ).

!!! Warning ""

    `Traitlets` defines its own classes, resp. support creation of user specific types but do not rely on python's typing system as e.g. [`pydantic`](https://pydantic-docs.helpmanual.io/)

Types (`C`-prefixed type are casted):

- **Numbers**: `Int` (aliased as `Integer`), `Long`, `Float`, `Complex`, `CInt`, `CLong`, `CFloat`, `CComplex`
- **Strings**: `Unicode`, `Bytes`, `Cunicode`, `CBytes`, `ObjectName`, `DottedObjectName`
- **Containers** : `List`, `Set`, `Tuple`, `Dict`
- **Classes and Instances**: `Instance`, `Type`, `This`, `ForwardDeclaredInstance`, `ForwardDeclaredType`
- **Misc**: `Bool`, `CBool`, `Enum`, `CaselessStrEnum`, `UseEnum`, `TCPAddress`, `CRegExp`, `Union`, `Callable`, `Any` 


??? Example

    <script src="https://gist.github.com/fesaille/26f128a1ea33d6cb5c3e7bcb8231e5b1.js"></script>



## Messaging in Jupyter

<badge-doc href='https://jupyter-client.readthedocs.io/en/stable/messaging.html'></badge-doc> 
