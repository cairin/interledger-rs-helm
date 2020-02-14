<p align="center">
  <img src="docs/interledger-rs.svg" width="700" alt="Interledger.rs">
</p>

---
> Helm charts for [Interledger implementation in Rust](https://github.com/interledger-rs/interledger-rs) :money_with_wings:

## Prerequisites

- [Redis](https://redis.io/)

## Installation

The [configuration parameters](https://github.com/interledger-rs/interledger-rs/blob/master/docs/configuration.md#configuration-parameters) of the ilp-node are configured using [environment variables](https://github.com/interledger-rs/interledger-rs/blob/master/docs/configuration.md#environment-variables) using a ConfigMap in kubernetes. The config object in [values.yaml](./values.yaml) correlates to the aforementioned configuration parameters.

### Setting the configurations

```
$ helm install \
     --namespace your_namespace \
     --generate-name \
     --set config.secret_seed=$(openssl rand -hex 32) \
     --set config.admin_auth_token=$(openssl rand -base64 16) \
     --set config.database_url=redis://:password@redis-master:port/ \
     interledger-rs/ilp-node
```

### Deviations

#### http_bind_address
In the specified configuration parameters:

```
http_bind_address: 127.0.0.1:7770
```

In values.yaml:

```
http_server:
  address: 127.0.0.1
  port: 7770
```