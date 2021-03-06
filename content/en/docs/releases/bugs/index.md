---
title: Reporting Bugs
description: What to do if you find a bug.
weight: 34
aliases:
    - /bugs.html
    - /bugs/index.html
    - /help/bugs/
    - /about/bugs
    - /latest/about/bugs
owner: istio/wg-docs-maintainers
test: n/a
---

Oh no! You found a bug? We'd love to hear about it.

## Product bugs

Search our [issue database](https://github.com/istio/istio/issues/) to see if
we already know about your problem and learn about when we think we can fix
it. If you don't find your problem in the database, please open a [new
issue](https://github.com/istio/istio/issues/new/choose) and let us know
what's going on.

If you think a bug is in fact a security vulnerability, please visit [Reporting Security Vulnerabilities](/docs/releases/security-vulnerabilities/)
to learn what to do.

### Kubernetes cluster state archives

If you're running on Kubernetes, consider including a cluster state
archive with your bug report.
For convenience, you can run the `istioctl bug-report` command to produce an archive containing
all of the relevant state from your Kubernetes cluster:

    {{< text bash >}}
    $ istioctl bug-report
    {{< /text >}}

Then attach the produced `bug-report.tgz` with your reported problem.

{{< tip >}}
The `istioctl bug-report` command is only available with `istioctl` version `1.8.0` and higher but it can be used to also collect the information from an older Istio version installed in your cluster.
{{< /tip >}}

If you are unable to use the `bug-report` command, please attach your own archive
containing:

* Pods, services, deployments, and endpoints across all namespaces:

    {{< text bash >}}
    $ kubectl get pods,services,deployments,endpoints --all-namespaces -o yaml > k8s_resources.yaml
    {{< /text >}}

* Secret names in `istio-system`:

    {{< text bash >}}
    $ kubectl --namespace istio-system get secrets
    {{< /text >}}

* configmaps in the `istio-system` namespace:

    {{< text bash >}}
    $ kubectl --namespace istio-system get cm -o yaml
    {{< /text >}}

* Current and previous logs from all Istio components and sidecar

* Istiod logs:

    {{< text bash >}}
    $ kubectl logs -n istio-system -l app=istiod
    {{< /text >}}

* All Istio configuration artifacts:

    {{< text bash >}}
    $ kubectl get $(kubectl get crd  --no-headers | awk '{printf "%s,",$1}END{printf "attributemanifests.config.istio.io\n"}') --all-namespaces
    {{< /text >}}

## Documentation bugs

Search our [documentation issue database](https://github.com/istio/istio.io/issues/) to see if
we already know about your problem and learn about when we think we can fix it. If you don't
find your problem in the database, please [report the issue there](https://github.com/istio/istio.io/issues/new).
If you want to submit a proposed edit to a page, you will find an "Edit this Page on GitHub"
link at the bottom right of every page.
