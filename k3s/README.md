This README will guide you through the setup of a K3s cluster on your system.

# Setup

## Note Before

In some host systems, including OpenSUSE Tumbleweed, one will need to disable
firewalld to ensure proper functioning of k3s and its pods.

This is something we intend figuring out in the near future.

## From the internet

One can easily setup k3s with s3gw from the internet, by running

```
$ curl -sfL https://raw.githubusercontent.com/aquarist-labs/s3gw-core/main/k3s/setup.sh | sh -
```

## From source repository

To install a lightweight Kubernetes cluster for development purpose run
the following commands. It will install open-iscsi and K3s on your local
system. Additionally, it will deploy Longhorn and the s3gw in the cluster.

```
$ cd ~/git/s3gw-core/k3s
$ ./setup.sh
```

# Access the Longhorn UI

The Longhorn UI can be access via the URL `http://localhost:80/longhorn/`.

# Access the S3 API

The S3 API can be accessed via `localhost:80/s3gw`.

We provide a [s3cmd](https://github.com/s3tools/s3cmd) configuration file
to easily communicate with the S3 gateway in the k3s cluster.

```
$ cd ~/git/s3gw-core/k3s
$ s3cmd -c ./s3cmd.cfg mb s3://foo
$ s3cmd -c ./s3cmd.cfg ls s3://
```

Please adapt the `host_base` and `host_bucket` properties in the `s3cmd.cfg`
configuration file if your K3s cluster is not accessible via localhost.

# Configure s3gw as Longhorn backup target

Use the following values in the Longhorn settings page to use the s3gw as
backup target.

Backup Target: `s3://<BUCKET_NAME>@us/`
Backup Target Credential Secret: `s3gw-secret`