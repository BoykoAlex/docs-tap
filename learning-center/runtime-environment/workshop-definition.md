# Workshop resource

The ``Workshop`` custom resource defines a workshop.

The raw CRD <!-- Shorten to |CRD| after first use. -->for the ``Workshop`` custom resource can be<!-- Consider switching to active voice. --> viewed at:

- [https://github.com/eduk8s/eduk8s/blob/develop/resources/crds-v1/workshop.yaml](https://github.com/eduk8s/eduk8s/blob/develop/resources/crds-v1/workshop.yaml) <!-- Type |in GitHub| somewhere in the cross-reference sentence. -->

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Workshop title and description

Each workshop is required to provide the ``title`` and ``description`` fields. If the fields are not supplied, the ``Workshop`` resource will be rejected when you attempt to load it into the Kubernetes cluster.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-markdown-sample
spec:
  title: Markdown Sample
  description: A sample workshop using Markdown
  content:
    files: github.com/eduk8s/lab-markdown-sample
```

The ``title`` field should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> be a single line value giving the subject of the workshop.

The ``description`` field should be a longer description of the workshop.

The following optional information can also be supplied for the workshop.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-markdown-sample
spec:
  title: Markdown Sample
  description: A sample workshop using Markdown
  url: https://github.com/eduk8s/lab-markdown-sample
  difficulty: beginner
  duration: 15m
  vendor: eduk8s.io
  authors:
  - John Smith
  tags:
  - template
  logo: data:image/png;base64,....
  content:
    files: github.com/eduk8s/lab-markdown-sample
```

The ``url<!-- |URL| is preferred. -->`` field should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> be a URL you can go to for more information about the workshop.

The ``difficulty`` field should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> give an indication of who the workshop is targeting. The value must be one of ``beginner``, ``intermediate``, ``advanced`` and ``extreme``<!-- Insert the Oxford comma if it is missing here. -->.

The ``duration`` field gives the expected<!-- Consider replacing with |in most cases| to sound more confident. --> maximum amount of time the workshop would<!-- Re-phrase for present tense if possible. --> take to complete. This field only provides informational value and is not used to police how long a workshop instance will<!-- Avoid |will|: present tense is preferred. --> last. The format of the field is an integer number with ``s``, ``m``, or ``h`` suffix.

The ``vendor`` field should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> be a value which identifies the company or organization which the authors are affiliated with. This could<!-- |can| or |might| whenever possible is preferred. When providing examples, use simple present tense verbs instead of postulating what someone or something could or would do. --> be a company or organization name, or a DNS hostname<!-- |host name| is preferred. --> under the control of whoever has created the workshop.

The ``authors`` field should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> list the people who worked on creating the workshop.

The ``tags`` field should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> list labels which help to identify what the workshop is about. This will<!-- Avoid |will|: present tense is preferred. --> be used in a searchable catalog of workshops.

The ``logo`` field should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> be a graphical image provided in embedded data URI format which depicts the topic of the workshop. The image should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> be 400 by 400 pixels. This will<!-- Avoid |will|: present tense is preferred. --> be used in a searchable catalog of workshops.

Note<!-- Format the note properly. --> that<!-- Notes must be in Note boxes and start with |Note: |. --> when referring to a workshop definition after it has been<!-- Consider changing to |is| or |has| or rewrite for active voice. --> loaded into a Kubernetes cluster, the value of ``name`` field given in the metadata is used. If you want<!-- Avoid anthropomorphizing by writing that software |wants| anything. --> to<!-- Maybe replace with just |To|. --> play around with slightly different variations of a workshop, copy the original workshop definition YAML file and change the value of ``name``. Then<!-- Remove |Then| at the beginning of task steps. The sequence of events is already clear. --> make your changes and load it into the Kubernetes cluster.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Downloading workshop content

Workshop content can be<!-- Consider switching to active voice. --> downloaded at the time the workshop instance is created. Provided the amount of content is not too great, this shouldn't<!-- In most cases, replace with |must not|. If using |should not| is unavoidable, it must be paired with information on the exceptions that |should not| implies exist. --> affect<!-- Consider using a more precise verb. --> startup times for the workshop instance. The alternative is to bundle the workshop content in a container image built from the Learning Center workshop base image.

To download workshop content at the time the workshop instance is started, set the ``content.files`` field to the location of the workshop content.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-markdown-sample
spec:
  title: Markdown Sample
  description: A sample workshop using Markdown
  content:
    files: github.com/eduk8s/lab-markdown-sample
```

The location can be<!-- Consider switching to active voice. --> a GitHub or GitLab repository reference, a URL to a tarball hosted on a HTTP server, or a reference to an OCI image artifact on a registry.

In the case of a GitHub or GitLab repository, do not prefix the location with ``https://`` as a symbolic reference is being used and not an actual URL.

The format of the reference to a GitHub or GitLab repository is similar to that used with kustomize when referencing remote repositories. For example:

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`github.com/organisation/project`` - Use the workshop content hosted at the root of the GitHub repository. The ``master<!-- Preferred alternatives: |primary|, |controller|. Other alternatives: |main|, |original|, |reference|, |control plane|, |control plane node|. -->`` or ``main`` branch is used.

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`github.com/organisation/project/subdir?ref=develop`` - Use the workshop content hosted at ``subdir`` of the GitHub repository. The ``develop`` branch is used.

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`gitlab.com/organisation/project`` - Use the workshop content hosted at the root of the GitLab repository. The ``master<!-- Preferred alternatives: |primary|, |controller|. Other alternatives: |main|, |original|, |reference|, |control plane|, |control plane node|. -->`` branch is used.

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`gitlab.com/organisation/project/subdir?ref=develop`` - Use the workshop content hosted at ``subdir`` of the GitLab repository. The ``develop`` branch is used.

In the case of a URL to a tarball hosted on a HTTP server, the URL can be<!-- Consider switching to active voice. --> in the following formats:

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`https://example.com/workshop.tar<!-- |TAR| is preferred. -->`` - Use the workshop content from the top level directory of the unpacked tarball.

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`https://example.com/workshop.tar<!-- |TAR| is preferred. -->.gz`` - Use the workshop content from the top level directory of the unpacked tarball.

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`https://example.com/workshop.tar<!-- |TAR| is preferred. -->?path=subdir`` - Use the workshop content from the specified sub directory path of the unpacked tarball.

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`https://example.com/workshop.tar<!-- |TAR| is preferred. -->.gz?path=subdir`` - Use the workshop content from the specified sub directory path of the unpacked tarball.

The tarball referenced by the URL can be<!-- Consider switching to active voice. --> uncompressed or compressed.

If using GitHub, instead of using the earlier form for referencing the Git repository containing the workshop content, you can instead use a URL to refer directly to the downloadable tarball for a specific version of the Git repository.

 <!-- When introducing a bullet, end with a colon. -->* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`https://github.com/organization/project/archive/develop.tar<!-- |TAR| is preferred. -->.gz?path=project-develop``

When using this form you must reference the ``.tar<!-- |TAR| is preferred. -->.gz`` download and cannot use the ``.zip`` file. The base name of the tarball file is the branch or commit name. You must specify<!-- Use as a general term to instruct users when they have several selections to make. Do not use in procedures when a more specific term, such as enter, select, or click, is appropriate. --> the ``path`` query string parameter where the argument is the name of the project and branch or commit. The path needs to<!-- |must| is preferred. --> be supplied as the contents of the repository is not returned at the root of the archive.

If using GitLab, it also provides a means of download a package as a tarball.

 <!-- When introducing a bullet, end with a colon. -->* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`https://gitlab.com/organization/project/-/archive/develop/project-develop.tar<!-- |TAR| is preferred. -->.gz?path=project-develop``

If the GitHub or GitLab repository is private, you can generate a personal access token providing read only access to the repository and include the credentials in the URL.

 <!-- When introducing a bullet, end with a colon. -->* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`https://username<!-- |user name| is preferred. -->@token:github.com/organization/project/archive/develop.tar<!-- |TAR| is preferred. -->.gz?path=project-develop``

As with this method a full URL is being supplied to request a tarball of the repository, and not referring to the repository itself, you can also reference private enterprise versions of GitHub or GitLab and the repository doesn't need to<!-- |must| is preferred. --> be on the public ``github.com`` or ``gitlab.com`` sites.

The last case is a reference to an OCI image artifact stored on a registry. This is not a full container image with operating system, but an image containing just<!-- Avoid uses that suggest a task is simple. --> the files making up the workshop content. The URI formats for this is:

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`imgpkg+https://harbor.example.com/organisation/project:version`` - Use the workshop content from the top level directory of the unpacked OCI artifact. The registry in this case must support ``https``.

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`imgpkg+https://harbor.example.com/organisation/project:version?path=subdir`` - Use the workshop content from the specified sub directory path of the unpacked OCI artifact. The registry in this case must support ``https``.

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`imgpkg+http://harbor.example.com/organisation/project:version`` - Use the workshop content from the top level directory of the unpacked OCI artifact. The registry in this case can support only ``http``.

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`imgpkg+http://harbor.example.com/organisation/project:version?path=subdir`` - Use the workshop content from the specified sub directory path of the unpacked OCI artifact. The registry in this case can support only ``http``.

Instead of the prefix ``imgpkg+https://``, you can instead use just<!-- Avoid uses that suggest a task is simple. --> ``imgpkg://``. The registry in this case must still support ``https``.

For any of the formats, credentials can be<!-- Consider switching to active voice. --> supplied as part of the URI.

 <!-- When introducing a bullet, end with a colon. -->* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`imgpkg+https://username<!-- |user name| is preferred. -->:password@harbor.example.com/organisation/project:version``

Access to the registry using a secure connection using ``https`` must have a valid certificate.

The OCI image artficact can be<!-- Consider switching to active voice. --> created using ``imgpkg`` from the Carvel tool set. For example, from the top level directory of the Git repository containing the workshop content you would run:

```
imgpkg push -i harbor.example.com/organisation/project:version -f .
```

In all cases for downloading workshop content, the ``workshop`` sub directory holding the actual workshop content, will<!-- Avoid |will|: present tense is preferred. --> be relocated to ``/opt/workshop`` so that it is not visible to a user. If you want<!-- Avoid anthropomorphizing by writing that software |wants| anything. --> other files ignored and not included in<!-- Consider deleting |included|. --> what the user can see<!-- Avoid anthropomorphizing: |detect| might be better here. -->, you can supply a ``.eduk8signore`` file in your repository or tarball and list patterns for the files in it.

Note<!-- Format the note properly. --> that<!-- Notes must be in Note boxes and start with |Note: |. --> the contents of the ``.eduk8signore`` file is processed as a list of patterns and each will<!-- Avoid |will|: present tense is preferred. --> be applied recursively to subdirectories. To ensure that a file is only ignored if it resides in the root directory, you need<!-- Avoid anthropomorphizing: |require| might be better here. --> to prefix it with ``./``.

```
./.dockerignore
./.gitignore
./Dockerfile
./LICENSE
./README.md
./kustomization.yaml
./resources
``` <!-- Define any non-obvious placeholders present in the code snippet in the style of |Where PLACEHOLDER is...| -->

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Container image for the workshop

When workshop content is bundled into a container image, the ``content.image`` field should specify the image reference identifying the location of the container image to be deployed for the workshop instance.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-markdown-sample
spec:
  title: Markdown Sample
  description: A sample workshop using Markdown
  content:
    image: quay.io/eduk8s/lab-markdown-sample:master
```

Even if using the ability to<!-- |can| is shorter. Avoid nounification of verbs where possible. --> download workshop content when the workshop environment is started, you may<!-- |can| usually works better. Use |might| to convey possibility. --> still want to override the workshop image used as a base. This would<!-- Re-phrase for present tense if possible. --> be done where you have a custom workshop base image that includes additional language runtimes<!-- |runtime durations| or |runtime environments| is preferred, depending on meaning. --> or tools required by specialized workshops.

For example, if running a Java workshop, you could<!-- |can| or |might| whenever possible is preferred. When providing examples, use simple present tense verbs instead of postulating what someone or something could or would do. --> specify<!-- Use as a general term to instruct users when they have several selections to make. Do not use in procedures when a more specific term, such as enter, select, or click, is appropriate. --> the ``jdk11-environment`` workshop image, with workshop content still pulled down from GitHub.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-spring-testing
spec:
  title: Spring Testing
  description: Playground for testing Spring development
  content:
    image: projects.registry.vmware.com/educates/jdk11-environment:latest
    files: github.com/eduk8s-tests/lab-spring-testing
```

Note<!-- Format the note properly. --> that<!-- Notes must be in Note boxes and start with |Note: |. --> if wanting to use the latest version of an image, always include the ``:latest`` tag. This is important because the Learning Center operator will<!-- Avoid |will|: present tense is preferred. --> look for version tags ``:main``, ``:master<!-- Preferred alternatives: |primary|, |controller|. Other alternatives: |main|, |original|, |reference|, |control plane|, |control plane node|. -->``, ``:develop`` and ``:latest``, and when they are used will<!-- Avoid |will|: present tense is preferred. --> set the image pull policy to ``Always`` to ensure that a newer version is always pulled if available, otherwise the image will<!-- Avoid |will|: present tense is preferred. --> be cached on the Kubernetes nodes and only pulled when it is initially not present. Any other version tags will<!-- Avoid |will|: present tense is preferred. --> always be assumed to be unique and never updated. Do though be aware<!-- To avoid anthropomorphism, use |detects|. --> of image registries which use a CDN as front end. When using these image tags the CDN can still always regard them as unique and they will<!-- Avoid |will|: present tense is preferred. --> not do pull through<!-- Do not use as a synonym for |finished| or |done|. Do not use when you mean |by using|. --> requests to update an image even if uses a tag of ``:latest``.

Where special custom workshop base images are available as part of the Learning Center project, instead of specifying the full location for the image, including the image registry, you can specify a short name. The Learning Center operator will then fill in the rest of the details.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-spring-testing
spec:
  title: Spring Testing
  description: Playground for testing Spring development
  content:
    image: jdk11-environment:latest
    files: github.com/eduk8s-tests/lab-spring-testing
```

The short versions of the names which are recognized are:

* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`base-environment:*`` - A tagged version of the ``base-environment`` workshop image which has been<!-- Consider changing to |is| or |has| or rewrite for active voice. --> matched with the current version of the Learning Center operator.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`jdk8-environment:*`` - A tagged version of the ``jdk8-environment`` workshop image which has been<!-- Consider changing to |is| or |has| or rewrite for active voice. --> matched with the current version of the Learning Center operator.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`jdk11-environment:*`` - A tagged version of the ``jdk11-environment`` workshop image which has been<!-- Consider changing to |is| or |has| or rewrite for active voice. --> matched with the current version of the Learning Center operator.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`conda-environment:*`` - A tagged version of the ``conda-environment`` workshop image which has been<!-- Consider changing to |is| or |has| or rewrite for active voice. --> matched with the current version of the Learning Center operator.

The ``*`` variants of the short names map to the most up to date version of the image which was available at the time that the version of the Learning Center operator was released. That version is thus<!-- Re-write the sentence to drop |thus| or, if that is not possible, replace with |therefore|. --> guaranteed to work with that version of the Learning Center operator, where as ``latest`` version may<!-- |can| usually works better. Use |might| to convey possibility. --> be newer, with possible incompatibilities.

Note<!-- Format the note properly. --> that<!-- Notes must be in Note boxes and start with |Note: |. --> if required, the short names can be<!-- Consider switching to active voice. --> remapped in the ``SystemProfile`` configuration of the Learning Center operator. Additional short names can also be defined which map to your own custom workshop base images for use in your own deployment of the Learning Center operator, along with<!-- Do not use as a conjunction. Whenever possible, use |with| or |and| instead. --> any workshop of your own.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Setting environment variables

If you want to<!-- Maybe replace with just |To|. --> set or override environment variables for the workshop instance, you can supply the ``session.env<!-- |environment| is preferred -->`` field.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-markdown-sample
spec:
  title: Markdown Sample
  description: A sample workshop using Markdown
  content:
    files: github.com/eduk8s/lab-markdown-sample
  session:
    env:
    - name: REPOSITORY_URL
      value: https://github.com/eduk8s/lab-markdown-sample
``` <!-- Define any non-obvious placeholders present in the code snippet in the style of |Where PLACEHOLDER is...| -->

The ``session.env<!-- |environment| is preferred -->`` field should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> be a list of dictionaries with ``name`` and ``value`` fields.

Values of fields in the list of resource objects can reference a number of pre-defined parameters. The available parameters are:

* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`session_id`` - A unique ID for the workshop instance within the workshop environment.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`session_namespace`` - The namespace created for and bound to the workshop instance. This is the namespace unique to the session and where a workshop can create their own resources.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`environment_name`` - The name of the workshop environment. For now this is the same as the name of the namespace for the workshop environment. Don't rely on them being the same, and use the most appropriate to cope with any future<!-- Only document what exists. There are legal ramifications to making promises. --> change.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`workshop_namespace`` - The namespace for the workshop environment. This is the namespace where all deployments of the workshop instances are created, and where the service account that the workshop instance runs as exists.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`service_account`` - The name of the service account the workshop instance runs as, and which has access to the namespace created for that workshop instance.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`ingress_domain`` - The host domain under which hostnames<!-- |host names| is preferred. --> can be<!-- Consider switching to active voice. --> created when creating ingress routes.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`ingress_protocol`` - The protocol (http/https) that is used for ingress routes which are created for workshops.

The syntax for referencing one of the parameters is ``$(parameter_name)``.

Note<!-- Format the note properly. --> that<!-- Notes must be in Note boxes and start with |Note: |. --> the ability to<!-- |can| is shorter. Avoid nounification of verbs where possible. --> override environment variables using this field should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> be limited to cases where they are required for the workshop. If you want to<!-- Maybe replace with just |To|. --> set or override an environment for a specific workshop environment, use the ability to<!-- |can| is shorter. Avoid nounification of verbs where possible. --> set environment variables in the ``WorkshopEnvironment`` custom resource for the workshop environment instead.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Overriding the memory available

By default the container the workshop environment is running in is allocated 512Mi. If the editor is enabled a total of 1Gi is allocated.

Where the purpose of the workshop is mainly aimed at deploying workloads into the Kubernetes cluster, this would<!-- Re-phrase for present tense if possible. --> generally be sufficient<!-- |suffice| is punchier. -->. If you are running workloads in the workshop environment container itself and need more memory, the default can be<!-- Consider switching to active voice. --> overridden by setting ``memory`` under ``session.resources``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-markdown-sample
spec:
  title: Markdown Sample
  description: A sample workshop using Markdown
  content:
    image: quay.io/eduk8s/lab-markdown-sample:master
  session:
    resources:
      memory: 2Gi
```

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Mounting a persistent volume

In circumstances where a workshop needs persistent storage to ensure no loss of work if the workshop environment container were killed and restarted, you can request a persistent volume be mounted into the workshop container.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-markdown-sample
spec:
  title: Markdown Sample
  description: A sample workshop using Markdown
  content:
    image: quay.io/eduk8s/lab-markdown-sample:master
  session:
    resources:
      storage: 5Gi
```

The persistent volume will<!-- Avoid |will|: present tense is preferred. --> be mounted on top of the ``/home/eduk8s`` directory. Because this would<!-- Re-phrase for present tense if possible. --> hide any workshop content bundled with the image, an init container is automatically<!-- Avoid if not definitely useful to mention. --> configured and run, which will<!-- Avoid |will|: present tense is preferred. --> copy the contents of the home directory to the persistent volume, before the persistent volume is then mounted on top of the home directory.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Resource budget for namespaces

In conjunction with each workshop instance, a namespace will<!-- Avoid |will|: present tense is preferred. --> be created for use during the workshop. That is, from the terminal of the workshop dashboard applications can be<!-- Consider switching to active voice. --> deployed into the namespace via<!-- |through|, |using| and |by means of| are preferred. --> the Kubernetes REST API using tools such as ``kubectl` <!-- Do not format |kubectl| as code. -->`.

By default this namespace will<!-- Avoid |will|: present tense is preferred. --> have whatever limit ranges and resource quota may<!-- |can| usually works better. Use |might| to convey possibility. --> be enforced by<!-- Active voice is preferred. --> the Kubernetes cluster. In most case this will<!-- Avoid |will|: present tense is preferred. --> mean there are no limits or quotas.

To control how much resources can be<!-- Consider switching to active voice. --> used where no limit ranges and resource quotas are set, or to override any default limit ranges and resource quota, you can set a resource budget for any namespaces created for the workshop instance.

To set the resource budget, set the ``session.namespaces.budget`` field.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-markdown-sample
spec:
  title: Markdown Sample
  description: A sample workshop using Markdown
  content:
    image: quay.io/eduk8s/lab-markdown-sample:master
  session:
    namespaces:
      budget: small
```

The resource budget sizings and quotas for CPU and memory are:

``` <!-- Define any non-obvious placeholders present in the code snippet in the style of |Where PLACEHOLDER is...| -->
| Budget    | CPU   | Memory |
| <!-- Insert |_n/a_| within purposefully empty cells. -->-----------|-------|--------|
| <!-- Insert |_n/a_| within purposefully empty cells. --> small     | 1000m | 1Gi    |
| <!-- Insert |_n/a_| within purposefully empty cells. --> medium    | 2000m | 2Gi    |
| <!-- Insert |_n/a_| within purposefully empty cells. --> large     | 4000m | 4Gi    |
| <!-- Insert |_n/a_| within purposefully empty cells. --> x-large   | 8000m | 8Gi    |
| <!-- Insert |_n/a_| within purposefully empty cells. --> xx-large  | 8000m | 12Gi   |
| <!-- Insert |_n/a_| within purposefully empty cells. --> xxx-large | 8000m | 16Gi   |
```

A value of 1000m is equivalent to 1 CPU.

Separate resource quotas for CPU and memory are applied for terminating and non terminating workloads.

Only the CPU and memory quotas are listed above, but limits are also in place on the number of resource objects that can be created of certain types, including persistent volume claims, replication controllers, services and secrets.

For each budget type, a limit range is created with fixed defaults. The limit ranges for CPU usage on a container are as follows.

``` <!-- Define any non-obvious placeholders present in the code snippet in the style of |Where PLACEHOLDER is...| -->
| Budget    | Min | Max   | Request | Limit |
| <!-- Insert |_n/a_| within purposefully empty cells. -->-----------|-----|-------|---------|-------|
| <!-- Insert |_n/a_| within purposefully empty cells. --> small     | 50m | 1000m | 50m     | 250m  |
| <!-- Insert |_n/a_| within purposefully empty cells. --> medium    | 50m | 2000m | 50m     | 500m  |
| <!-- Insert |_n/a_| within purposefully empty cells. --> large     | 50m | 4000m | 50m     | 500m  |
| <!-- Insert |_n/a_| within purposefully empty cells. --> x-large   | 50m | 8000m | 50m     | 500m  |
| <!-- Insert |_n/a_| within purposefully empty cells. --> xx-large  | 50m | 8000m | 50m     | 500m  |
| <!-- Insert |_n/a_| within purposefully empty cells. --> xxx-large | 50m | 8000m | 50m     | 500m  |
```

Those for memory are:

```
| Budget    | Min  | Max  | Request | Limit |
| <!-- Insert |_n/a_| within purposefully empty cells. -->-----------|------|------|---------|-------|
| <!-- Insert |_n/a_| within purposefully empty cells. --> small     | 32Mi | 1Gi  | 128Mi   | 256Mi |
| <!-- Insert |_n/a_| within purposefully empty cells. --> medium    | 32Mi | 2Gi  | 128Mi   | 512Mi |
| <!-- Insert |_n/a_| within purposefully empty cells. --> large     | 32Mi | 4Gi  | 128Mi   | 1Gi   |
| <!-- Insert |_n/a_| within purposefully empty cells. --> x-large   | 32Mi | 8Gi  | 128Mi   | 2Gi   |
| <!-- Insert |_n/a_| within purposefully empty cells. --> xx-large  | 32Mi | 12Gi | 128Mi   | 2Gi   |
| <!-- Insert |_n/a_| within purposefully empty cells. --> xxx-large | 32Mi | 16Gi | 128Mi   | 2Gi   |
```

The request and limit values are the defaults applied to a container when no resources specification is given in a pod<!-- |Pod| is capitalized per the K8s docs style. --> specification.

If a budget sizing for CPU and memory is sufficient, but you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> override the limit ranges and defaults for request and limit values when none is given in a pod<!-- |Pod| is capitalized per the K8s docs style. --> specification, you can supply overrides in ``session.namespaces.limits``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-markdown-sample
spec:
  title: Markdown Sample
  description: A sample workshop using Markdown
  content:
    image: quay.io/eduk8s/lab-markdown-sample:master
  session:
    namespaces:
      budget: medium
      limits:
        min:
          cpu: 50m
          memory: 32Mi
        max:
          cpu: 1
          memory: 1Gi
        defaultRequest:
          cpu: 50m
          memory: 128Mi
        default:
          cpu: 500m
          memory: 1Gi
```

Although all possible properties that can be<!-- Consider switching to active voice. --> set are listed in this example, you only need to<!-- |must| is preferred. --> supply the property for the value you want to override.

If you need more control over limit ranges and resource quotas, you should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> set the resource budget to ``custom``. This will<!-- Avoid |will|: present tense is preferred. --> remove any default limit ranges and resource quota which might be applied to the namespace. You can then specify<!-- Use as a general term to instruct users when they have several selections to make. Do not use in procedures when a more specific term, such as enter, select, or click, is appropriate. --> your own ``LimitRange`` and ``ResourceQuota`` resources as part of the list of resources created for each session.

Before disabling the quota and limit ranges, or contemplating any switch to using a custom set of ``LimitRange`` and ``ResourceQuota`` resources, consider if that is what is really required. The default requests defined by these for memory and CPU are fallbacks only. In most cases instead of changing the defaults, you should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> specify<!-- Use as a general term to instruct users when they have several selections to make. Do not use in procedures when a more specific term, such as enter, select, or click, is appropriate. --> memory and CPU resources in the pod<!-- |Pod| is capitalized per the K8s docs style. --> template specification of your deployment resources used in the workshop, to indicate what the application actually<!-- Delete unless referring to a situation that is actual instead of virtual. Most uses are extraneous. --> requires. This will<!-- Avoid |will|: present tense is preferred. --> allow you to control exactly what the application is able to<!-- |can| is preferred. --> use and so fit into the minimum quota required for the task.

Note<!-- Format the note properly. --> that<!-- Notes must be in Note boxes and start with |Note: |. --> this budget setting and the memory values are distinct from the amount of memory the container the workshop environment runs in. If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> change how much memory is available to the workshop container, set the ``memory`` setting under ``session.resources``.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Patching workshop deployment

In order to set or override environment variables you can provide ``session.env<!-- |environment| is preferred -->``. If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> make other changes to the pod<!-- |Pod| is capitalized per the K8s docs style. --> template for the deployment used to create the workshop instance, you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> provide an overlay patch. Such a patch might be used to override the default CPU and memory limit applied to the workshop instance, or to mount a volume.

The patches are provided by setting ``session.patches``. The patch will<!-- Avoid |will|: present tense is preferred. --> be applied to the ``spec<!-- |specifications| is preferred. -->`` field of the pod template.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-resource-testing
spec:
  title: Resource testing
  description: Play area for testing memory resources
  content:
    files: github.com/eduk8s-tests/lab-resource-testing
  session:
    patches:
      containers:
      - name: workshop
        resources:
          requests:
            memory: "1Gi"
          limits:
            memory: "1Gi"
```

In this example the default memory limit of "512Mi" is increased to "1Gi". Although memory is being set via<!-- |through|, |using| and |by means of| are preferred. --> a patch in this example, the ``session.resources.memory`` field is the preferred way to override the memory allocated to the container the workshop environment is running in.

The patch when applied works a bit differently to overlay patches as found elsewhere in Kubernetes. Specifically, when patching an array and the array contains a list of objects, a search is performed on the destination array and if an object already exists with the same value for the ``name`` field, the item <!-- Rewrite to avoid or use |that is,| instead. Note the comma. -->in the source array will<!-- Avoid |will|: present tense is preferred. --> be overlaid on top of the existing item <!-- Rewrite to avoid or use |that is,| instead. Note the comma. -->in the destination array. If there is no matching item <!-- Rewrite to avoid or use |that is,| instead. Note the comma. -->in the destination array, the item <!-- Rewrite to avoid or use |that is,| instead. Note the comma. -->in the source array will<!-- Avoid |will|: present tense is preferred. --> be added to the end of the destination array.

This means an array doesn't outright replace an existing array, but a more intelligent merge is performed of elements in the array.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Creation of session resources

When a workshop instance is created, the deployment running the workshop dashboard is created in the namespace for the workshop environment. When more than one workshop instance is created under that workshop environment, all those deployments are in the same namespace.

For each workshop instance, a separate empty namespace is created with name corresponding to the workshop session. The workshop instance is configured so that the service account that the workshop instance runs under can access and create resources in the namespace created for that workshop instance. Each separate workshop instance has its own corresponding namespace and they can't see the namespace for another instance.

If you want to<!-- Maybe replace with just |To|. --> pre-create additional resources within the namespace for a workshop instance, you can supply a list of the resources against the ``session.objects`` field within the workshop definition. You might use this to add additional custom roles to the service account for the workshop instance when working in that namespace, or to deploy a distinct instance of an application for just that workshop instance, such as a private image registry.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-registry-testing
spec:
  title: Registry Testing
  description: Play area for testing image registry
  content:
    files: github.com/eduk8s-tests/lab-registry-testing
  session:
    objects:
    - apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: registry
      spec:
        replicas: 1
        selector:
          matchLabels:
            deployment: registry
        strategy:
          type: Recreate
        template:
          metadata:
            labels:
              deployment: registry
          spec:
            containers:
            - name: registry
              image: registry.hub.docker.com/library/registry:2.6.1
              imagePullPolicy: IfNotPresent
              ports:
              - containerPort: 5000
                protocol: TCP
              env:
              - name: REGISTRY_STORAGE_DELETE_ENABLED
                value: "true"
    - apiVersion: v1
      kind: Service
      metadata:
        name: registry
      spec:
        type: ClusterIP
        ports:
        - port: 80
          targetPort: 5000
        selector:
          deployment: registry
``` <!-- Define any non-obvious placeholders present in the code snippet in the style of |Where PLACEHOLDER is...| -->

Note<!-- Format the note properly. --> that<!-- Notes must be in Note boxes and start with |Note: |. --> for namespaced resources, it is not necessary to specify<!-- Use as a general term to instruct users when they have several selections to make. Do not use in procedures when a more specific term, such as enter, select, or click, is appropriate. --> the ``namespace`` field of the resource ``metadata``. When the ``namespace`` field is not present the resource will<!-- Avoid |will|: present tense is preferred. --> automatically<!-- Avoid if not definitely useful to mention. --> be created within the session namespace for that workshop instance.

When resources are created, owner references are added making the ``WorkshopSession`` custom resource corresponding to the workshop instance the owner. This means that when the workshop instance is deleted, any resources will<!-- Avoid |will|: present tense is preferred. --> be automatically<!-- Avoid if not definitely useful to mention. --> deleted.

Values of fields in the list of resource objects can reference a number of pre-defined parameters. The available parameters are:

* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`session_id`` - A unique ID for the workshop instance within the workshop environment.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`session_namespace`` - The namespace created for and bound to the workshop instance. This is the namespace unique to the session and where a workshop can create their own resources.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`environment_name`` - The name of the workshop environment. For now this is the same as the name of the namespace for the workshop environment. Don't rely on them being the same, and use the most appropriate to cope with any future<!-- Only document what exists. There are legal ramifications to making promises. --> change.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`workshop_namespace`` - The namespace for the workshop environment. This is the namespace where all deployments of the workshop instances are created, and where the service account that the workshop instance runs as exists.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`service_account`` - The name of the service account the workshop instance runs as, and which has access to the namespace created for that workshop instance.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`ingress_domain`` - The host domain under which hostnames<!-- |host names| is preferred. --> can be<!-- Consider switching to active voice. --> created when creating ingress routes.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`ingress_protocol`` - The protocol (http/https) that is used for ingress routes which are created for workshops.

The syntax for referencing one of the parameters is ``$(parameter_name)``.

In the case of cluster scoped resources, it is important that you set the name of the created resource so that it embeds the value of ``$(session_namespace)``. This way the resource name is unique to the workshop instance and you will<!-- Avoid |will|: present tense is preferred. --> not get a clash with a resource for a different workshop instance.

For examples of making use of the available parameters see the following sections.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Overriding default RBAC rules

By default the service account created for the workshop instance, has ``admin`` role access to the session namespace created for that workshop instance. This enables the service account to be used to deploy applications to the session namespace, as well as<!-- |and| is preferred. --> manage secrets and service accounts.

Where a workshop doesn't require ``admin`` access for the namespace, you can reduce the level of access it has to ``edit`` or ``view`` by setting the ``session.namespaces.role`` field.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-role-testing
spec:
  title: Role Testing
  description: Play area for testing roles
  content:
    files: github.com/eduk8s-tests/lab-role-testing
  session:
    namespaces:
      role: view
```

If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> add additional roles to the service account, such as the ability to<!-- |can| is shorter. Avoid nounification of verbs where possible. --> work with custom resource types which have been<!-- Consider replacing with |were| or shifting to present tense. --> added to the cluster, you can add the appropriate ``Role`` and ``RoleBinding`` definitions to the ``session.objects`` field described previously.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-kpack-testing
spec:
  title: Kpack Testing
  description: Play area for testing kpack
  content:
    files: github.com/eduk8s-tests/lab-kpack-testing
  session:
    objects:
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: Role
      metadata:
        name: kpack-user
      rules:
      - apiGroups:
        - build.pivotal.io
        resources:
        - builds
        - builders
        - images
        - sourceresolvers
        verbs:
        - get
        - list
        - watch
        - create
        - delete
        - patch
        - update
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: RoleBinding
      metadata:
        name: kpack-user
      roleRef:
        apiGroup: rbac.authorization.k8s.io
        kind: Role
        name: kpack-user
      subjects:
      - kind: ServiceAccount
        namespace: $(workshop_namespace)
        name: $(service_account)
```

Because the subject of a ``RoleBinding`` needs to<!-- |must| is preferred. --> specify<!-- Use as a general term to instruct users when they have several selections to make. Do not use in procedures when a more specific term, such as enter, select, or click, is appropriate. --> the service account name and namespace it is contained within, both of which are unknown in advance, references to parameters for the workshop namespace and service account for the workshop instance are used when defining the subject.

Adding additional resources via<!-- |through|, |using| and |by means of| are preferred. --> ``session.objects`` can also be used to grant cluster level roles, which would<!-- Re-phrase for present tense if possible. --> be necessary if you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> grant the service account ``cluster-admin`` role.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-admin-testing
spec:
  title: Admin Testing
  description: Play area for testing cluster admin
  content:
    files: github.com/eduk8s-tests/lab-admin-testing
  session:
    objects:
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: ClusterRoleBinding
      metadata:
        name: $(session_namespace)-cluster-admin
      roleRef:
        apiGroup: rbac.authorization.k8s.io
        kind: ClusterRole
        name: cluster-admin
      subjects:
      - kind: ServiceAccount
        namespace: $(workshop_namespace)
        name: $(service_account)
```

In this case the name of the cluster role binding resource embeds ``$(session_namespace)`` so that its name is unique to the workshop instance and doesn't overlap with a binding for a different workshop instance.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Running user containers as root

In addition to RBAC which controls what resources a user can create and work with, pod<!-- |Pod| is capitalized per the K8s docs style. --> security policies are applied to restrict what pods<!-- |Pods| is capitalized per the K8s docs style. -->/containers<!-- If this is a URL then you likely need to present it per xref rules: https://docs-wiki.cfapps.io/wiki/style/cross-ref-style.html --> a user deploys can do.

By default the deployments that can be<!-- Consider switching to active voice. --> created by<!-- Active voice is preferred. --> a workshop user are only allowed to run containers as a non root user. This means that many container images available on registries such as Docker Hub may<!-- |can| usually works better. Use |might| to convey possibility. --> not be able to<!-- |can| is preferred. --> be used.

If you are creating a workshop where a user needs to<!-- |must| is preferred. --> be able to<!-- |can| is preferred. --> run containers as the root user, you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> override the default ``nonroot`` security policy and select the ``anyuid`` security policy using the ``session.namespaces.security.policy`` setting.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-policy-testing
spec:
  title: Policy Testing
  description: Play area for testing security policies
  content:
    files: github.com/eduk8s-tests/lab-policy-testing
  session:
    namespaces:
      security:
        policy: anyuid
```

This setting applies to the primary session namespace and any secondary namespaces that may<!-- |can| usually works better. Use |might| to convey possibility. --> be created.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Creating additional namespaces

For each workshop instance a primary session namespace is created, into which applications can be<!-- Consider switching to active voice. --> pre-deployed, or deployed as part of the workshop.

If you need more than one namespace per workshop instance, you can create secondary namespaces in a couple of ways.

If the secondary namespaces are to be created empty, you can list the details of the namespaces under the property ``session.namespaces.secondary``.

```
    apiVersion: training.eduk8s.io/v1alpha2
    kind: Workshop
    metadata:
      name: lab-namespace-testing
    spec:
      title: Namespace Testing
      description: Play area for testing namespaces
      content:
        files: github.com/eduk8s-tests/lab-namespace-testing
      session:
        namespaces:
          role: admin
          budget: medium
          secondary:
          - name: $(session_namespace)-apps
            role: edit
            budget: large
            limits:
              default:
                memory: 512mi
```

When secondary namespaces are created, by default, the role, resource quotas and limit ranges will<!-- Avoid |will|: present tense is preferred. --> be set the same as the primary session namespace. Each namespace will<!-- Avoid |will|: present tense is preferred. --> though have a separate resource budget, it is not shared.

If required, you can override what ``role``, ``budget`` and ``limits``<!-- Insert the Oxford comma if it is missing here. --> should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> be applied within the entry for the namespace.

Similarly, you can override the security policy for secondary namespaces on a case by case basis by adding the ``security.policy`` setting under the entry for the secondary namespace.

If you also need to<!-- |must| is preferred. --> create resources in the namespaces you want to create, you may<!-- |can| usually works better. Use |might| to convey possibility. --> prefer creating the namespaces by adding an appropriate ``Namespace`` resource to ``session.objects``, along with the definitions of the resources you want to create in the namespaces.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-namespace-testing
spec:
  title: Namespace Testing
  description: Play area for testing namespaces
  content:
    files: github.com/eduk8s-tests/lab-namespace-testing
  session:
    objects:
    - apiVersion: v1
      kind: Namespace
      metadata:
        name: $(session_namespace)-apps
```

When listing any other resources to be created within the additional namespace, such as deployments, ensure that the ``namespace`` is set in the ``metadata`` of the resource, e.g., ``$(session_namespace)-apps``.

If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> override what role the service account for the workshop instance has in the additional namespace, you can set the ``training.eduk8s.io/session.role`` annotation on the ``Namespace`` resource.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-namespace-testing
spec:
  title: Namespace Testing
  description: Play area for testing namespaces
  content:
    files: github.com/eduk8s-tests/lab-namespace-testing
  session:
    objects:
    - apiVersion: v1
      kind: Namespace
      metadata:
        name: $(session_namespace)-apps
        annotations:
          training.eduk8s.io/session.role: view
```

If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> have a different resource budget set for the additional namespace, you can add the annotation ``training.eduk8s.io/session.budget`` in the ``Namespace`` resource metadata and set the value to the required resource budget.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-namespace-testing
spec:
  title: Namespace Testing
  description: Play area for testing namespaces
  content:
    files: github.com/eduk8s-tests/lab-namespace-testing
  session:
    objects:
    - apiVersion: v1
      kind: Namespace
      metadata:
        name: $(session_namespace)-apps
        annotations:
          training.eduk8s.io/session.budget: large
```

In order to override the limit range values applied corresponding to the budget applied, you can add annotations starting with ``training.eduk8s.io/session.limits.`` for each entry.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-namespace-testing
spec:
  title: Namespace Testing
  description: Play area for testing namespaces
  content:
    files: github.com/eduk8s-tests/lab-namespace-testing
  session:
    objects:
    - apiVersion: v1
      kind: Namespace
      metadata:
        name: $(session_namespace)-apps
        annotations:
          training.eduk8s.io/session.limits.min.cpu: 50m
          training.eduk8s.io/session.limits.min.memory: 32Mi
          training.eduk8s.io/session.limits.max.cpu: 1
          training.eduk8s.io/session.limits.max.memory: 1Gi
          training.eduk8s.io/session.limits.defaultrequest.cpu: 50m
          training.eduk8s.io/session.limits.defaultrequest.memory: 128Mi
          training.eduk8s.io/session.limits.request.cpu: 500m
          training.eduk8s.io/session.limits.request.memory: 1Gi
```

You only need to<!-- |must| is preferred. --> supply annotations for the values you want to override.

If you need more fine grained control over the limit ranges and resource quotas, set the value of the annotation for the budget to ``custom`` and add the ``LimitRange`` and ``ResourceQuota`` definitions to ``session.objects``.

In this case you must set the ``namespace`` for the ``LimitRange`` and ``ResourceQuota`` resource to the name of the namespace, e.g., ``$(session_namespace)-apps`` so they are only applied to that namespace.

If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> set the security policy for a specific namespace different to the primary session namespace, you can add the annotation ``training.eduk8s.io/session.security.policy`` in the ``Namespace`` resource metadata and set the value to ``nonroot`` or ``anyuid`` as necessary.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Shared workshop resources

Adding a list of resources to ``session.objects`` will<!-- Avoid |will|: present tense is preferred. --> result in the given resources being created for each workshop instance, where namespaced resources will<!-- Avoid |will|: present tense is preferred. --> default to being created in the session namespace for that workshop instance.

If instead you want to have one common shared set of resources created once for the whole workshop environment, that is, used by all workshop instances, you can list them in the ``environment.objects`` field.

This might for example <!-- Consider adding a comma after |for example|. -->be used to deploy a single image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. --> which is used by<!-- Active voice is preferred. --> all workshop instances, with a Kubernetes job used to import a set of images into the image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. -->, which are then referenced by the workshop instances.

For namespaced resources, it is not necessary to specify<!-- Use as a general term to instruct users when they have several selections to make. Do not use in procedures when a more specific term, such as enter, select, or click, is appropriate. --> the ``namespace`` field of the resource ``metadata``. When the ``namespace`` field is not present the resource will<!-- Avoid |will|: present tense is preferred. --> automatically<!-- Avoid if not definitely useful to mention. --> be created within the workshop namespace for that workshop environment.

When resources are created, owner references are added making the ``WorkshopEnvironment`` custom resource corresponding to the workshop environment the owner. This means that when the workshop environment is deleted, any resources will<!-- Avoid |will|: present tense is preferred. --> be automatically<!-- Avoid if not definitely useful to mention. --> deleted.

Values of fields in the list of resource objects can reference a number of pre-defined parameters. The available parameters are:

* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`workshop_name`` - The name of the workshop. This is the name of the ``Workshop`` definition the workshop environment was created against.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`environment_name`` - The name of the workshop environment. For now this is the same as the name of the namespace for the workshop environment. Don't rely on them being the same, and use the most appropriate to cope with any future<!-- Only document what exists. There are legal ramifications to making promises. --> change.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`environment_token`` - The value of the token which needs to<!-- |must| is preferred. --> be used in workshop requests against the workshop environment.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`workshop_namespace`` - The namespace for the workshop environment. This is the namespace where all deployments of the workshop instances, and their service accounts, are created. It is the same namespace that shared workshop resources are created.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`service_account`` - The name of a service account that can be<!-- Consider switching to active voice. --> used when creating deployments in the workshop namespace.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`ingress_domain`` - The host domain under which hostnames<!-- |host names| is preferred. --> can be<!-- Consider switching to active voice. --> created when creating ingress routes.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`ingress_protocol`` - The protocol (http/https) that is used for ingress routes which are created for workshops.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`ingress_secret`` - The name of the ingress secret stored in the workshop namespace when secure ingress is being used.

If you want to<!-- Maybe replace with just |To|. --> create additional namespaces associated with the workshop environment, embed a reference to ``$(workshop_namespace)`` in the name of the additional namespaces, with an appropriate suffix. Be mindful that the suffix doesn't overlap with the range of session IDs for workshop instances.

When creating deployments in the workshop namespace, set the ``serviceAccountName`` of the ``Deployment`` resouce to ``$(service_account)``. This will<!-- Avoid |will|: present tense is preferred. --> ensure the deployment makes use of a special pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy set up by the Learning Center. If this isn't used and the cluster imposes a more strict default pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy, your deployment may<!-- |can| usually works better. Use |might| to convey possibility. --> not work, especially if any image expects to run as ``root``.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Workshop pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy

The pod<!-- |Pod| is capitalized per the K8s docs style. --> for the workshop session will<!-- Avoid |will|: present tense is preferred. --> be setup with a pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy which restricts what can be<!-- Consider switching to active voice. --> done from containers in the pod<!-- |Pod| is capitalized per the K8s docs style. -->. The nature of the applied pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy will<!-- Avoid |will|: present tense is preferred. --> be adjusted when enabling support for doing docker<!-- |Docker| is preferred. --> builds to enable the ability to<!-- |can| is shorter. Avoid nounification of verbs where possible. --> do docker<!-- |Docker| is preferred. --> builds inside the side car container attached to the workshop container.

If you are customising the workshop by patching the pod<!-- |Pod| is capitalized per the K8s docs style. --> specification using ``session.patches``, in order to<!-- |to| is preferred. --> add your own side car container, and that side car container needs to<!-- |must| is preferred. --> run as the root user, or needs a custom pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy, you will<!-- Avoid |will|: present tense is preferred. --> need to<!-- |must| is preferred. --> override the default security policy for the workshop container.

In the case where you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> allow a side car container to run as the root user and no extra privileges are required, you can override the default ``nonroot`` security policy and set it to ``anyuid``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-policy-testing
spec:
  title: Policy Testing
  description: Play area for testing security policies
  content:
    files: github.com/eduk8s-tests/lab-policy-testing
  session:
    security:
      policy: anyuid
```

Note<!-- Format the note properly. --> that<!-- Notes must be in Note boxes and start with |Note: |. --> this is a different setting than that described previously for changing the security policy for deployments made by a workshop user to the session namespaces. This setting only applies to the workshop container itself.

If you need more fine grained control of the security policy you will<!-- Avoid |will|: present tense is preferred. --> need to<!-- |must| is preferred. --> provide your own resources for defining the pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy and map it so it is used. The details of the pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy will<!-- Avoid |will|: present tense is preferred. --> need to<!-- |must| is preferred. --> be included in<!-- Consider deleting |included|. --> ``environment.objects`` and mapped by definitions added to ``session.objects``. For this to be used, you will<!-- Avoid |will|: present tense is preferred. --> need<!-- Avoid anthropomorphizing: |require| might be better here. --> to disable<!-- |deactivate| is preferred. --> the application of the inbuilt pod<!-- |Pod| is capitalized per the K8s docs style. --> security policies. This can be<!-- Consider switching to active voice. --> done by setting ``session.security.policy`` to ``custom``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-policy-testing
spec:
  title: Policy Testing
  description: Play area for testing policy override
  content:
    files: github.com/eduk8s-tests/lab-policy-testing
  session:
    security:
      policy: custom
    objects:
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: RoleBinding
      metadata:
        namespace: $(workshop_namespace)
        name: $(session_namespace)-podman
      roleRef:
        apiGroup: rbac.authorization.k8s.io
        kind: ClusterRole
        name: $(workshop_namespace)-podman
      subjects:
      - kind: ServiceAccount
        namespace: $(workshop_namespace)
        name: $(service_account)
  environment:
    objects:
    - apiVersion: policy/v1beta1
      kind: PodSecurityPolicy
      metadata:
        name: aa-$(workshop_namespace)-podman
      spec:
        privileged: true
        allowPrivilegeEscalation: true
        requiredDropCapabilities:
        - KILL
        - MKNOD
        hostIPC: false
        hostNetwork: false
        hostPID: false
        hostPorts: []
        runAsUser:
          rule: MustRunAsNonRoot
        seLinux:
          rule: RunAsAny
        fsGroup:
          rule: RunAsAny
        supplementalGroups:
          rule: RunAsAny
        volumes:
        - configMap
        - downwardAPI
        - emptyDir
        - persistentVolumeClaim
        - projected
        - secret
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: ClusterRole
      metadata:
        name: $(workshop_namespace)-podman
      rules:
      - apiGroups:
        - policy
        resources:
        - podsecuritypolicies
        verbs:
        - use
        resourceNames:
        - aa-$(workshop_namespace)-podman
``` <!-- Define any non-obvious placeholders present in the code snippet in the style of |Where PLACEHOLDER is...| -->

By overriding the pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy you are responsible for limiting what can be<!-- Consider switching to active voice. --> done from the workshop pod<!-- |Pod| is capitalized per the K8s docs style. -->. In other words, you should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> only add just<!-- Avoid uses that suggest a task is simple. --> the extra capabilities you need. The pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy will<!-- Avoid |will|: present tense is preferred. --> only be applied to the pod<!-- |Pod| is capitalized per the K8s docs style. --> the workshop session runs in, it does not affect<!-- Consider using a more precise verb. --> any pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy applied to service accounts which exist in the session namespace or other namespaces which have been<!-- Consider replacing with |were| or shifting to present tense. --> created.

Note<!-- Format the note properly. --> that<!-- Notes must be in Note boxes and start with |Note: |. --> due to a lack of a good way to deterministically determine<!-- |determine| has two meanings. Consider if the univocal |discover| or |verify| would be better. --> priority of applied pod<!-- |Pod| is capitalized per the K8s docs style. --> security policies when a default pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy has been<!-- Consider changing to |is| or |has| or rewrite for active voice. --> applied globally by mapping it to the ``system:authenticated`` group, with priority instead falling back to ordering of the names of the pod<!-- |Pod| is capitalized per the K8s docs style. --> security policies, it is recommend you use ``aa-`` as a prefix to the custom pod<!-- |Pod| is capitalized per the K8s docs style. --> security name you create. This will<!-- Avoid |will|: present tense is preferred. --> ensure that it take precedence over any global default pod<!-- |Pod| is capitalized per the K8s docs style. --> security policy such as ``restricted``, ``pks-restricted`` or ``vmware<!-- |VMware| is preferred. -->-system-tmc-restricted``, no matter what the name of the global policy default is called.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Defining additional ingress points

If running additional background applications, by default they are only accessible to other processes within the same container. In order for an application to be accessible to a user via<!-- |through|, |using| and |by means of| are preferred. --> their web browser, an ingress needs to<!-- |must| is preferred. --> be created mapping to the port for the application.

You can do this by supplying a list of the ingress points, and the internal container port they map to, by setting the ``session.ingresses`` field in the workshop definition.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    ingresses:
    - name: application
      port: 8080
```

The form of the hostname used in URL to access the service will be:

``` <!-- Define any non-obvious placeholders present in the code snippet in the style of |Where PLACEHOLDER is...| -->
$(session_namespace)-application.$(ingress_domain)
```

Note<!-- Format the note properly. --> that<!-- Notes must be in Note boxes and start with |Note: |. --> you should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> not use as the name, the name of any built-in dashboards, ``terminal``, ``console``, ``slides`` or ``editor``<!-- Insert the Oxford comma if it is missing here. -->. These are reserved for the corresponding built-in capabilities providing those features.

In addition to specifying ingresses for proxying to internal ports within the same pod<!-- |Pod| is capitalized per the K8s docs style. -->, you can specify<!-- Use as a general term to instruct users when they have several selections to make. Do not use in procedures when a more specific term, such as enter, select, or click, is appropriate. --> a ``host``, ``protocol`` and ``port<!-- Insert the Oxford comma if it is missing here. -->`` corresponding to a separate service running in the Kubernetes cluster.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    ingresses:
    - name: application
      protocol: http
      host: service.namespace.svc.cluster.local
      port: 8080
```

Variables providing information about the current session can be<!-- Consider switching to active voice. --> used within the ``host`` property if required.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    ingresses:
    - name: application
      protocol: http
      host: service.$(session_namespace).svc.cluster.local
      port: 8080
```

The available variables are:

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`session_namespace`` - The namespace created for and bound to the workshop instance. This is the namespace unique to the session and where a workshop can create their own resources.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`environment_name`` - The name of the workshop environment. For now this is the same as the name of the namespace for the workshop environment. Don't rely on them being the same, and use the most appropriate to cope with any future<!-- Only document what exists. There are legal ramifications to making promises. --> change.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`workshop_namespace`` - The namespace for the workshop environment. This is the namespace where all deployments of the workshop instances are created, and where the service account that the workshop instance runs as exists.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`ingress_domain`` - The host domain under which hostnames<!-- |host names| is preferred. --> can be<!-- Consider switching to active voice. --> created when creating ingress routes.

If the service uses standard ``http`` or ``https`` ports, you can leave out the ``port`` property and the port will<!-- Avoid |will|: present tense is preferred. --> be set based on the value of ``protocol``.

When a request is being proxied, you can specify additional request headers that should be passed to the service.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    ingresses:
    - name: application
      protocol: http
      host: service.$(session_namespace).svc.cluster.local
      port: 8080
      headers:
      - name: Authorization
        value: "Bearer $(kubernetes_token)"
```

The value of a header can reference the following variables.

 <!-- When introducing a bullet, end with a colon. -->* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`kubernetes_token`` - The access token of the service account for the current workshop session, used for accessing the Kubernetes REST API.

Accessing any service via<!-- |through|, |using| and |by means of| are preferred. --> the ingress will<!-- Avoid |will|: present tense is preferred. --> be protected by<!-- Active voice is preferred. --> any access controls enforced by the workshop environment or training portal. If the training portal is used this should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> be transparent, otherwise you will<!-- Avoid |will|: present tense is preferred. --> need to<!-- |must| is preferred. --> supply any login credentials for the workshop again when prompted by your web browser.  

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->External workshop instructions

In place of using workshop instructions provided with the workshop content, you can use externally hosted instructions instead. To do this set ``sessions.applications.workshop.url<!-- |URL| is preferred. -->`` to the URL of an external web site.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      workshop:
        url: https://www.example.com/instructions
```

The external web site must be able to<!-- |can| is preferred. --> displayed in an HTML iframe, will<!-- Avoid |will|: present tense is preferred. --> be shown as is and should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> provide its own page navigation and table of contents if required.

The URL value can reference a number of pre-defined parameters. The available parameters are:

* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`session_namespace`` - The namespace created for and bound to the workshop instance. This is the namespace unique to the session and where a workshop can create their own resources.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`environment_name`` - The name of the workshop environment. For now this is the same as the name of the namespace for the workshop environment. Don't rely on them being the same, and use the most appropriate to cope with any future<!-- Only document what exists. There are legal ramifications to making promises. --> change.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`workshop_namespace`` - The namespace for the workshop environment. This is the namespace where all deployments of the workshop instances are created, and where the service account that the workshop instance runs as exists.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`ingress_domain`` - The host domain under which hostnames<!-- |host names| is preferred. --> can be<!-- Consider switching to active voice. --> created when creating ingress routes.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`ingress_protocol`` - The protocol (http/https) that is used for ingress routes which are created for workshops.

These could be used for example to reference workshops instructions hosted as part of the workshop environment.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      workshop:
        url: $(ingress_protocol)://$(workshop_namespace)-instructions.$(ingress_domain)
  environment:
    objects:
    - ...
```

In this case ``environment.objects`` of the workshop ``spec<!-- |specifications| is preferred. -->`` would<!-- Re-phrase for present tense if possible. --> need to<!-- |must| is preferred. --> include resources to deploy the application hosting the instructions and expose it via<!-- |through|, |using| and |by means of| are preferred. --> an appropriate ingress.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Disabling workshop instructions

The aim of the workshop environment is to provide instructions for a workshop which users can follow. If you want instead to use the workshop environment as a development environment<!-- If this simply refers to the user machine, |local machine| is preferred. If drawing a distinction from a production environment, leave as is. -->, or use it as an administration console which provides access to a Kubernetes cluster, you can disable<!-- |deactivate| is preferred. --> the display of workshop instructions provided with the workshop content. In this case only the work area with the terminals, console, etc.<!-- |and so on| is preferred. -->, will<!-- Avoid |will|: present tense is preferred. --> be displayed. To disable<!-- |deactivate| is preferred. --> display of workshop instructions, add a ``session.applications.workshop`` section and set the ``enabled`` property to ``false``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      workshop:
        enabled: false
```

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Enabling the Kubernetes console

By default the Kubernetes console is not enabled. If you want to<!-- Maybe replace with just |To|. --> enable it and make it available through<!-- Do not use as a synonym for |finished| or |done|. Do not use when you mean |by using|. --> the web browser when accessing a workshop, you need<!-- Avoid anthropomorphizing: |require| might be better here. --> to add a ``session.applications.console`` section to the workshop definition, and set the ``enabled`` property to ``true``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      console:
        enabled: true
```

The Kubernetes dashboard provided by the Kubernetes project will<!-- Avoid |will|: present tense is preferred. --> be used. If you would<!-- Re-phrase for present tense if possible. --> rather use Octant as the console, you can set the ``vendor`` property to ``octant``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      console:
        enabled: true
        vendor: octant
```

When ``vendor`` is not set, ``kubernetes<!-- |Kubernetes| is preferred. -->`` is assumed.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Enabling the integrated editor

By default the integrated web based editor is not enabled. If you want to<!-- Maybe replace with just |To|. --> enable it and make it available through<!-- Do not use as a synonym for |finished| or |done|. Do not use when you mean |by using|. --> the web browser when accessing a workshop, you need<!-- Avoid anthropomorphizing: |require| might be better here. --> to add a ``session.applications.editor`` section to the workshop definition, and set the ``enabled`` property to ``true``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      editor:
        enabled: true
```

The integrated editor which is used is based on VS Code. Details of the editor can be<!-- Consider switching to active voice. --> found at:

* [https://github.com/cdr/code-server](https://github.com/cdr/code-server) <!-- Type |in GitHub| somewhere in the cross-reference sentence. -->

If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> install additional VS Code extensions, this can be<!-- Consider switching to active voice. --> done from the editor. Alternatively, if building a custom workshop, you can install them from your ``Dockerfile`` into your workshop image by running:

```
code-server --install-extension vendor.extension
```

Replace ``vendor.extension`` with the name of the extension, where the name identifies the extension on the VS Code extensions marketplace used by the editor, or provide a path name to a local ``.vsix`` file.

This will<!-- Avoid |will|: present tense is preferred. --> install the extensions into ``$HOME/.config/code-server/extensions``.

If downloading extensions yourself and unpacking them, or you have them as part of your Git repository, you can instead locate them in the ``workshop/code-server/extensions`` directory.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Enabling workshop downloads

At times you may<!-- |can| usually works better. Use |might| to convey possibility. --> want to provide a way for a workshop user to download files which are provided as part of the workshop content. This capability can be<!-- Consider switching to active voice. --> enabled by<!-- Active voice is preferred. --> adding the ``session.applications.files`` section to the workshop definition, and setting the ``enabled`` property to ``true``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      files:
        enabled: true
```

The recommended way of providing access to files from workshop instructions is using the ``files:download-file`` clickable action block. This action will<!-- Avoid |will|: present tense is preferred. --> ensure any file is downloaded to the local machine and not simply<!-- Avoid suggesting an instruction is |simple| or |easy|. --> displayed in the browser in place of the workshop instructions.

By default any files located under the home directory of the workshop user account can be<!-- Consider switching to active voice. --> accessed. To restrict where files can be<!-- Consider switching to active voice. --> download from, set the ``directory`` setting.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      files:
        enabled: true
        directory: exercises
```

When the specified directory is a relative path, it is evaluated relative to the home directory of the workshop user.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Enabling the test examiner

The test examiner is a feature which allows a workshop to have verification checks which can be<!-- Consider switching to active voice. --> triggered from the workshop instructions. The test examiner is disabled<!-- |deactivated| is preferred. --> by default. If you want to<!-- Maybe replace with just |To|. --> enable it, you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> add a ``session.applications.examiner`` section to the workshop definition, and set the ``enabled`` property to ``true``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      examiner:
        enabled: true
```

Any executable<!-- Do not use as a noun. Use |executable file| instead. --> test programs to be used for verification checks need to<!-- |must| is preferred. --> be provided in the ``workshop/examiner/tests`` directory.

The test programs should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> return an exit status of 0 if the test is successful and non zero<!-- |nonzero| is preferred. --> if a failure. The test programs should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> not be persistent programs that would<!-- Re-phrase for present tense if possible. --> run forever.

Clickable actions for the test examiner are used within the workshop instructions to trigger the verification checks, or they can be<!-- Consider switching to active voice. --> configured to be automatically<!-- Avoid if not definitely useful to mention. --> started when the page of the workshop instructions is loaded.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Enabling session image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. -->

Workshops using tools such as ``kpack`` or ``tekton`` and which need a place to push container images when built, can enable an image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. -->. A separate image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. --> is deployed for each workshop session.

Note<!-- Format the note properly. --> that<!-- Notes must be in Note boxes and start with |Note: |. --> the image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. --> is only currently fully usable if workshops are deployed under an Learning Center operator configuration which uses secure ingress. This is because an insecure<!-- |not secure| is preferred. --> registry would<!-- Re-phrase for present tense if possible. --> not be trusted by<!-- Active voice is preferred. --> the Kubernetes cluster as the source of container images when doing deployments.

To enable the deployment of an image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. --> per workshop session you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> add a ``session.applications.registry`` section to the workshop definition, and set the ``enabled`` property to ``true``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      registry:
        enabled: true
```

The image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. --> will<!-- Avoid |will|: present tense is preferred. --> mount a persistent volume for storing of images. By default the size of that persistent volume is 5Gi. If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> override the size of the persistent volume add the ``storage`` property under the ``registry`` section.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      registry:
        enabled: true
        storage: 20Gi
```

The amount of memory provided to the image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. --> will<!-- Avoid |will|: present tense is preferred. --> default to 768Mi. If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> increase this, add the ``memory`` property under the ``registry`` section.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      registry:
        enabled: true
        memory: 1Gi
```

The image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. --> will<!-- Avoid |will|: present tense is preferred. --> be secured with a username<!-- |user name| is preferred. --> and password unique to the workshop session and expects access over a secure connection.

To allow access from the workshop session, the file ``$HOME/.docker<!-- |Docker| is preferred. -->/config.json<!-- |JSON| is preferred. -->`` containing the registry credentials will<!-- Avoid |will|: present tense is preferred. --> be injected into the workshop session. This will<!-- Avoid |will|: present tense is preferred. --> be automatically<!-- Avoid if not definitely useful to mention. --> used by tools such as ``docker<!-- |Docker| is preferred. -->``.

For deployments in Kubernetes, a secret of type ``kubernetes<!-- |Kubernetes| is preferred. -->.io/dockerconfigjson`` is created in the namespace and automatically<!-- Avoid if not definitely useful to mention. --> applied to the ``default`` service account in the namespace. This means deployments made using the default service account will<!-- Avoid |will|: present tense is preferred. --> be able to<!-- |can| is preferred. --> pull images from the image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. --> without additional configuration. If creating deployments using other service accounts, you will<!-- Avoid |will|: present tense is preferred. --> need to<!-- |must| is preferred. --> add configuration to the service account or deployment to add the registry secret for pulling images.

If you need access to the raw registry host details and credentials, they are provided as environment variables in the workshop session. The environment variables are:

* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`REGISTRY_HOST`` - Contains the host name for the image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. --> for the workshop session.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`REGISTRY_AUTH_FILE`` - Contains the location of the ``docker<!-- |Docker| is preferred. -->`` configuration file. Should<!-- In most cases, replace with |Must|. If using |Should| is unavoidable, it must be paired with information on the exceptions that |Should| implies exist. --> always be the equivalent of ``$HOME/.docker<!-- |Docker| is preferred. -->/config.json<!-- |JSON| is preferred. -->``.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`REGISTRY_USERNAME`` - Contains the username<!-- |user name| is preferred. --> for accessing the image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. -->.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`REGISTRY_PASSWORD`` - Contains the password for accessing the image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. -->. This will<!-- Avoid |will|: present tense is preferred. --> be different for each workshop session.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`REGISTRY_SECRET`` - Contains the name of a Kubernetes secret of type ``kubernetes<!-- |Kubernetes| is preferred. -->.io/dockerconfigjson`` added to the session namespace and which contains the registry credentials.

The URL for accessing the image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. --> adopts the HTTP protocol scheme inherited from the environment variable ``INGRESS_PROTOCOL``. This would<!-- Re-phrase for present tense if possible. --> be the same HTTP protocol scheme as the workshop sessions themselves use.

If you want to<!-- Maybe replace with just |To|. --> use any of the variables as data variables in workshop content, use the same variable name but in lower case<!-- |lowercase| is preferred. -->. Thus<!-- Re-write the sentence to drop |Thus| or, if that is not possible, replace with |therefore|. -->, ``registry_host``, ``registry_auth_file``, ``registry_username``, ``registry_password`` and ``registry_secret``.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Enabling ability to use Docker

If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> be able to<!-- |can| is preferred. --> build container images in a workshop using ``docker<!-- |Docker| is preferred. -->``, it needs<!-- Avoid anthropomorphizing: |requires| might be better here. --> to be enabled first. Each workshop session will<!-- Avoid |will|: present tense is preferred. --> be provided with its own separate docker<!-- |Docker| is preferred. --> daemon instance running in a container.

Note<!-- Format the note properly. --> that<!-- Notes must be in Note boxes and start with |Note: |. --> enabling of support for running ``docker<!-- |Docker| is preferred. -->`` requires the use of a privileged container for running the docker<!-- |Docker| is preferred. --> daemon. Because of the security implications of providing access to docker<!-- |Docker| is preferred. --> with this configuration, it is strongly<!-- Consider deleting, especially if it precedes |recommend|. --> recommended that if you don't trust the people doing the workshop, any workshops which require docker<!-- |Docker| is preferred. --> only be hosted in a disposable Kubernetes cluster which is destroyed at the completion of the workshop. You should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> never enable docker<!-- |Docker| is preferred. --> for workshops hosted on a public service which is always kept running and where arbitrary users could<!-- |can| or |might| whenever possible is preferred. When providing examples, use simple present tense verbs instead of postulating what someone or something could or would do. --> access the workshops.

To enable support for being able to<!-- |can| is preferred. --> use ``docker<!-- |Docker| is preferred. -->`` add a ``session.applications.docker<!-- |Docker| is preferred. -->`` section to the workshop definition, and set the ``enabled`` property to ``true``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      docker:
        enabled: true
```

The container which runs the docker<!-- |Docker| is preferred. --> daemon will<!-- Avoid |will|: present tense is preferred. --> mount a persistent volume for storing of images which are pulled down or built locally. By default the size of that persistent volume is 5Gi. If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> override the size of the persistent volume add the ``storage`` property under the ``docker<!-- |Docker| is preferred. -->`` section.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      docker:
        enabled: true
        storage: 20Gi
```

The amount of memory provided to the container running the docker<!-- |Docker| is preferred. --> daemon will<!-- Avoid |will|: present tense is preferred. --> default to 768Mi. If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> increase this, add the ``memory`` property under the ``registry`` section.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      docker:
        enabled: true
        memory: 1Gi
```

Access to the docker<!-- |Docker| is preferred. --> daemon from the workshop session uses a local UNIX<!-- |Unix| is preferred. --> socket shared with the container running the docker<!-- |Docker| is preferred. --> daemon. If using a local tool which wants to access the socket connection for the docker<!-- |Docker| is preferred. --> daemon directly rather than by running ``docker<!-- |Docker| is preferred. -->``, it should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> use the ``DOCKER_HOST`` environment variable to determine<!-- |determine| has two meanings. Consider if the univocal |discover| or |verify| would be better. --> the location of the socket.

The docker<!-- |Docker| is preferred. --> daemon is only available from within the workshop session and cannot be accessed outside of the pod<!-- |Pod| is capitalized per the K8s docs style. --> by any tools deployed separately to Kubernetes.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Enabling WebDAV access to files

Local files within the workshop session can be<!-- Consider switching to active voice. --> accessed or updated from the terminal<!-- Missing code tags? --> command line or editor of the workshop dashboard. The local files reside in the filesystem<!-- |file system| is preferred. --> of the container the workshop session is running in.

If there is a need to<!-- |must| is preferred. --> be able to<!-- |can| is preferred. --> access the files remotely, it is possible<!-- |might| might be better. --> to<!-- Active voice |you can| might be better. --> enable WebDAV support for the workshop session.

To enable support for being able to<!-- |can| is preferred. --> access files over WebDAV add a ``session.applications.webdav<!-- |WebDAV| is preferred. -->`` section to the workshop definition, and set the ``enabled`` property to ``true``.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      webdav:
        enabled: true
```

The result of this will<!-- Avoid |will|: present tense is preferred. --> be that a WebDAV server will<!-- Avoid |will|: present tense is preferred. --> be run within the workshop session environment. A set of credentials will<!-- Avoid |will|: present tense is preferred. --> also be automatically<!-- Avoid if not definitely useful to mention. --> generated which are available as environment variables. The environment variables are:

* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`WEBDAV_USERNAME`` - Contains the username<!-- |user name| is preferred. --> which needs to<!-- |must| is preferred. --> be used when authenticating over WebDAV.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`WEBDAV_PASSWORD`` - Contains the password which needs to<!-- |must| is preferred. --> be used authenticating over WebDAV.

If you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> use any of the environment variables related to the image registry<!-- If generic, |container image registry| on first use. If VMware-provided, |Tanzu Network Registry| on first use. In both cases, |registry| thereafter except where risking ambiguity. --> as data variables in workshop content, you will<!-- Avoid |will|: present tense is preferred. --> need to<!-- |must| is preferred. --> declare this in the ``workshop/modules.yaml`` file in the ``config.vars`` section.

```
config:
  vars:
  - name: WEBDAV_USERNAME
  - name: WEBDAV_PASSWORD
``` <!-- Define any non-obvious placeholders present in the code snippet in the style of |Where PLACEHOLDER is...| -->

The URL endpoint for accessing the WebDAV server is the same as the workshop session, with
`/webdav/` path added. This can be constructed from the terminal using:

```
$INGRESS_PROTOCOL://$SESSION_NAMESPACE.$INGRESS_DOMAIN/webdav/
``` <!-- Define any non-obvious placeholders present in the code snippet in the style of |Where PLACEHOLDER is...| -->

In workshop content it can be constructed using:

```
{{ingress_protocol}}://{{session_namespace}}.{{ingress_domain}}/webdav/
```

You should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> be able to<!-- |can| is preferred. --> use WebDAV client support provided by your operating system, of by using a standalone WebDAV client such as [CyberDuck](https://cyberduck.io/).

Using WebDAV can make it easier if you need<!-- Avoid anthropomorphizing: |require| might be better here. --> to transfer files to or from the workshop session.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Customizing the terminal layout

By default a single terminal is provided in the web browser when accessing the workshop. If required, you can enable alternate layouts which provide additional terminals. To set the layout, you need to<!-- Consider replacing with just |To|. --><!-- |must| is preferred. --> add the ``session.applications.terminal`` section and include the ``layout`` property with the desired layout.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    applications:
      terminal:
        enabled: true
        layout: split
```

The options for the ``layout`` property are:

* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`default`` - Single terminal.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`split`` - Two terminals stacked above<!-- IX Standards forbids referring to text |above|. Use |earlier| or, better, just an anchor. --> each other in ratio 60/40.<!-- If this is a URL then you likely need to present it per xref rules: https://docs-wiki.cfapps.io/wiki/style/cross-ref-style.html -->
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`split/2`` - Three terminals stacked above<!-- IX Standards forbids referring to text |above|. Use |earlier| or, better, just an anchor. --> each other in ratio 50/25<!-- If this is a URL then you likely need to present it per xref rules: https://docs-wiki.cfapps.io/wiki/style/cross-ref-style.html -->/25.
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`lower`` - A single terminal is placed below<!-- IX Standards forbids referring to text |below|. Use |following| or |later| or, better, just an anchor. --> any dashboard tabs, rather than being a tab<!-- Do not use as a verb. Replace with |navigate| or |select|, depending on context. --> of its own. The ratio of dashboard tab<!-- Do not use as a verb. Replace with |navigate| or |select|, depending on context. --> to terminal is 70/30.<!-- If this is a URL then you likely need to present it per xref rules: https://docs-wiki.cfapps.io/wiki/style/cross-ref-style.html -->
* `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`none`` - No terminal is displayed, but they can still be created from the drop down menu.

When adding the ``terminal`` section, you must include the ``enabled`` property and set it to ``true`` as it is a required field when including the section.

If you didn't want a terminal displayed, and also wanted to disable<!-- |deactivate| is preferred. --> the ability to<!-- |can| is shorter. Avoid nounification of verbs where possible. --> create terminals from the drop down menu, set ``enabled`` to ``false``.

##  <!-- Add an anchor ID unless you have reason not to: |<a id="NAME"></a>| -->Adding custom dashboard tabs

Exposed applications, external sites and additional terminals, can be given their own custom dashboard tab. This is done by specifying the list of dashboard panels and the target URL.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    ingresses:
    - name: application
      port: 8080
    dashboards:
    - name: Internal
      url: "$(ingress_protocol)://$(session_namespace)-application.$(ingress_domain)/"
    - name: External
      url: http://www.example.com
```

The URL values can reference a number of pre-defined parameters. The available parameters are:

- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`session_namespace`` - The namespace created for and bound to the workshop instance. This is the namespace unique to the session and where a workshop can create their own resources.
- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`environment_name`` - The name of the workshop environment. For now this is the same as the name of the namespace for the workshop environment. Don't rely on them being the same, and use the most appropriate to cope with any future<!-- Only document what exists. There are legal ramifications to making promises. --> change.
- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`workshop_namespace`` - The namespace for the workshop environment. This is the namespace where all deployments of the workshop instances are created, and where the service account that the workshop instance runs as exists.
- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`ingress_domain`` - The host domain under which hostnames<!-- |host names| is preferred. --> can be<!-- Consider switching to active voice. --> created when creating ingress routes.
- `<!-- Use |-| for bullet points. DocWorks is unreliable with |+| and |*|. -->`ingress_protocol`` - The protocol (http/https) that is used for ingress routes which are created for workshops.

The URL can reference an external web site, however, that web site must not prohibit being embedded in a HTML iframe.

In the case of wanting to have a custom dashboard tab<!-- Do not use as a verb. Replace with |navigate| or |select|, depending on context. --> provide an additional terminal, the ``url<!-- |URL| is preferred. -->`` property should<!-- In most cases, replace with |must|. If using |should| is unavoidable, it must be paired with information on the exceptions that |should| implies exist. --> use the form ``terminal:<session>``, where ``<session>`` is replaced with the name of the terminal session. The name of the terminal session can be any name you choose, but should be restricted to lower case letters, numbers and '-'. You should avoid using numeric terminal session names such as "1", "2" and "3" as these are use for the default terminal sessions.

```
apiVersion: training.eduk8s.io/v1alpha2
kind: Workshop
metadata:
  name: lab-application-testing
spec:
  title: Application Testing
  description: Play area for testing my application
  content:
    image: quay.io/eduk8s-tests/lab-application-testing:master
  session:
    dashboards:
    - name: Example
      url: terminal:example
```
