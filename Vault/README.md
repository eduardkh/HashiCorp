# HashiCorp Vault

> spin-up a dev server in a container (server side)

```bash
# vault dev server
docker run --cap-add=IPC_LOCK\
 -p 8200:8200\
 -e 'VAULT_DEV_LISTEN_ADDRESS=0.0.0.0:8200'\
 -e 'VAULT_DEV_ROOT_TOKEN_ID=root'\
 hashicorp/vault:1.14.2\
 vault server -dev
```

> install and setup the client (client side)

```bash
# install as root
apt-get update && apt-get upgrade
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
apt-get update && apt-get install vault

# add autocomplete
vault -autocomplete-install

# login with CLI
vault login token=root # or export VAULT_TOKEN="root"

# or export to environment variables
export VAULT_TOKEN="root"
export VAULT_ADDR="http://127.0.0.1:8200"
```

> transit (for auto unseal)

```bash
# enable transit engine
vault secrets enable transit
# create a key (for the child cluster to use)
vault write -f transit/keys/unseal-key
# attach a policy to the key
vault policy write unseal policy.hcl
# create a token
vault token create -policy=unseal
```
