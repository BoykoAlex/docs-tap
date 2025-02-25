# Install Spring Boot Conventions

This document describes how to install Spring Boot Conventions
from the Tanzu Application Platform package repository.

>**Note:** Use the instructions on this page if you do not want to use a profile to install packages.
Both the full and light profiles include Spring Boot Conventions.
For more information about profiles, see [Installing the Tanzu Application Platform Package and Profiles](../install.md).

## <a id='prereqs'></a>Prerequisites

Before installing Spring Boot Conventions:

- Complete all prerequisites to install Tanzu Application Platform. For more information, see [Prerequisites](../prerequisites.md).
- Ensure Convention Service is installed on the cluster. For more information, see the earlier
[Install Convention Service](../convention-service/install-convention-service.md#install-prereqs) section.

## <a id='install-spring-boot-conv'></a> Install Spring Boot Conventions

To install Spring Boot conventions:

1. Get the exact name and version information for the Spring Boot conventions package to be installed by running:

    ```
    tanzu package available list spring-boot-conventions.tanzu.vmware.com --namespace tap-install
    ```

    For example:

    ```
    $ tanzu package available list spring-boot-conventions.tanzu.vmware.com --namespace tap-install
    / Retrieving package versions for spring-boot-conventions.tanzu.vmware.com...
      NAME                                       VERSION   RELEASED-AT
      ...
      spring-boot-conventions.tanzu.vmware.com   0.1.2     2021-10-28T00:00:00Z
      ...
    ```

1. Install the package by running:

    ```
    tanzu package install spring-boot-conventions \
      --package-name spring-boot-conventions.tanzu.vmware.com \
      --version 0.1.2 \
      --namespace tap-install
    ```

1. Verify the package install by running:

    ```
    tanzu package installed get spring-boot-conventions --namespace tap-install
    ```

    For example:

    ```
    tanzu package installed get spring-boot-conventions -n tap-install
    | Retrieving installation details for spring-boot-conventions...
    NAME:                    spring-boot-conventions
    PACKAGE-NAME:            spring-boot-conventions.tanzu.vmware.com
    PACKAGE-VERSION:         0.1.2
    STATUS:                  Reconcile succeeded
    CONDITIONS:              [{ReconcileSucceeded True  }]
    USEFUL-ERROR-MESSAGE:
    ```

    Verify that `STATUS` is `Reconcile succeeded`
