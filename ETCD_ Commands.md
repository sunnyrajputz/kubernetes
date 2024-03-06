ETCDCTL is the CLI tool used to interact with ETCD.

ETCDCTL can interact wit  h ETCD Server using 2 API versions -  Version 2 and Version 3

By default its set to use Version 2. Each version has different sets of commands.
## For example ETCDCTL version 2 supports the following commands:
1. etcdctl backup
2. etcdctl cluster-health
3. etcdctl mk
4. etcdctl mkdir
5. etcdctl set

## Whereas the commands are different in version 3
1. etcdctl snapshot save
2. etcdctl endpoint health
3. etcdctl get
4. etcdctl put

## To set the right version of API set the environment variable ETCDCTL_API command

export ETCDCTL_API=3

When API version is not set, it is assumed to be set to version 2. And version 3 commands listed above don't work.
When API version is set to version 3, version 2 commands listed above don't work.
Apart from that, you must also specify path to certificate files so that ETCDCTL can authenticate to the ETCD API Server.
The certificate files are available in the etcd-master at the following path.
## We discuss more about certificates in the security section of this course. So don't worry if this looks complex:
1. --cacert /etc/kubernetes/pki/etcd/ca.crt
2. --cert /etc/kubernetes/pki/etcd/server.crt
3. --key /etc/kubernetes/pki/etcd/server.key
So for the commands I showed in the previous video to work you must specify the ETCDCTL API version and path to certificate files.
## Below is the final form:

kubectl exec etcd-master -n kube-system -- sh -c "ETCDCTL_API=3 etcdctl get / --prefix --keys-only --limit=10 --cacert 
/etc/kubernetes/pki/etcd/ca.crt 
--cert /etc/kubernetes/pki/etcd/server.crt 
  --key /etc/kubernetes/pki/etcd/server.key"
