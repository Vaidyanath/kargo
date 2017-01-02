Users and groups
================

There are following users and groups defined by the addusers role:

* Kube user, group from the ``kubelet_user`` and ``kubelet_group`` vars.
* Etcd user, group from the ``etcd_user`` and ``etcd_group`` vars.
* Network plugin user, group from the ``netplug_user`` and ``netplug_group`` vars.

There are additional certificate access groups for those users defined.
For example, kubelet and network plugins require read access to the
etcd certs and keys. This is defined via the corresponding ``etcd_cert_group``
var. Members of that group (defaults to `kube` and `netplug` users) will read
etcd secret keys and certs. Same rule applies to the ``kube_cert_group``
(defaults to `kube` user) and ``netplug_cert_group`` (defaults to `netplug`)
members.

Linux capabilites
=================

Kargo allows to drop some Linux capabilities for docker containers,
either those that stand for kubelet/etcd/networking systemd units or k8s
workloads being created as the part of the deployment process, like
kubedns or netchecker apps.

Dropped capabilites are represented by the ``apps_drop_cap``,
  ``etcd_drop_cap``, ``calico_drop_cap``, ``weave_drop_cap``,
``kubelet_drop_cap`` vars.

Note that etcd and network plugins' services are running in containers under
their own user ids matching the users described above. And kubelet wants
the root user rights inside of its container namespace.
