---
wrapper_template: "kubernetes/docs/base_docs.html"
markdown_includes:
  nav: "kubernetes/docs/shared/_side-navigation.md"
context:
  title: "CNI with flannel"
  description: How to manage and deploy Kubernetes with flannel
keywords: CNI, networking, flannel
tags: [operating]
sidebar: k8smain-sidebar
permalink: cni-flannel.html
layout: [base, ubuntu-com]
toc: False
---


[Flannel][] is a simple, lightweight layer 3 fabric for Kubernetes. Flannel manages an
IPv4 network between multiple nodes in a cluster. It does not control how containers
are networked to the host, only how the traffic is transported between hosts. For
more complicated scenarios, see also [Calico][] and [Canal][]


## Deploying **Charmed Kubernetes** with flannel

Flannel is the default choice for networking with **Charmed Kubernetes**. If you
[install using `conjure-up`][quickstart], or by
[manually deploying the bundle][install-manual] without changing the default settings,
flannel will be used for CNI.

## Flannel options


| Name                  |  Type     |  Default value | Description  |
|-----------------------|-----------|----------------|--------------|
| cidr                       | string     | 10.1.0.0/16      | Network CIDR to assign to Flannel  |
| iface                      | string     | see description>  |  The interface to bind flannel overlay networking. The default value is the interface bound to the CNI endpoint. |
|  nagios_context |  string |  juju  |  A string that will be prepended to instance name to set the host name in nagios. If you're running multiple environments with the same services in them this allows you to differentiate between them. Used by the nrpe subordinate charm. |
| nagios_servicegroups | string  | (empty)  | A comma-separated list of nagios servicegroups. If left empty, the `nagios_context` will be used as the servicegroup  |

### Checking the current configuration

To check the current configuration settings for Flannel, run the command:

```bash
juju config flannel
```

### Setting a config option

To set an option, simply run the config command with and additional `<key>=<value>` argument. For example, to set a specific network CIDR:

```bash
juju config flannel cidr="10.5.0.0/16"
```

## Troubleshooting

If there is an issue with connectivity, it can be useful to inspect the Juju logs. To
see a complete set of logs for flannel:

```bash
juju debug-log --replay --include=flannel
```

For additional troubleshooting pointers, please see the [dedicated troubleshooting page][troubleshooting].



<!-- LINKS -->

[Flannel]: https://github.com/coreos/flannel
[troubleshooting]: /kubernetes/docs/troubleshooting
[quickstart]:  /kubernetes/docs/quickstart
[install-manual]:  /kubernetes/docs/install-manual
[Calico]: /kubernetes/docs/cni-calico
[Canal]: /kubernetes/docs/cni-canal
