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

> regenerate a new root token (if lost)

```bash
# generate Nonce and OTP token
vault operator generate-root -init

# generate Encoded Token with Nonce and Unseal Key
vault operator generate-root -nonce=[Nonce] [Unseal Key]
vault operator generate-root -nonce=[Nonce] [Unseal Key]
vault operator generate-root -nonce=[Nonce] [Unseal Key]

# finally Root Token with OTP and Encoded Token
vault operator generate-root -otp=[OTP] -decode=[Encoded Token]
```

> or just start fresh (delete the old data)

```bash
sudo systemctl stop vault
sudo rm -rf /opt/vault/data/
sudo systemctl start vault

# Initialize Vault
vault operator init

# Unseal Vault
vault operator unseal [Key1]
vault operator unseal [Key2]
vault operator unseal [Key3]
```
