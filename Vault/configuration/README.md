# Vault configuration file

> start server with configuration (manual)

```bash
vault server -config /etc/vault.d/vault.hcl
```

> start server with systemd (as a service)

```bash
# create systemd service unit files
sudo nano /etc/systemd/system/vault.service
# reload and start systemd service
sudo systemctl daemon-reload
sudo systemctl enable vault
sudo systemctl start vault
sudo systemctl status vault
```

> initial steps (init and unseal)

```bash
# create a valid vault certificate (with SAN) or just use this
export VAULT_SKIP_VERIFY=true

# initiate vault
vault operator init

# unseal vault with 3 keys from the initiation step
vault operator unseal [Key1]
vault operator unseal [Key2]
vault operator unseal [Key3]
```
