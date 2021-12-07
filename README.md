# utils

## get prive IP from Cloud VM

### GCP

```bash
export PUBLIC_IP=$(curl -H "Metadata-Flavor: Google" http://metadata.google.internal/computeMetadata/v1/instance/network-interfaces/0/access-configs/0/external-ip)
```

### AZURE

```bash
export PUBLIC_IP=
```

### AWS

```bash
export PUBLIC_IP=curl http://169.254.169.254/latest/meta-data/public-ipv4
```

