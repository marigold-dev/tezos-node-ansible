# tezos-node-ansible

Project based on [ansible-role-tezos-baker of ECAD labs](https://github.com/ecadlabs/ansible-role-tezos-baker).

## How to execute

First, make sure you have ansible and docker installed on your machine:
* [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
* [Docker](https://docs.docker.com/engine/install/)


You will need write access on node folder volume, the default folder is inside of ~/tezos/

This is one way to do:
```
sudo chmod 777 -R hangzhounet_client
sudo chmod 777 -R hangzhounet_node
# or
sudo chmod 777 -R mainnet_client
sudo chmod 777 -R mainnet_node
```

Get the repository and enter the folder:
``` bash
git clone https://github.com/marigold-dev/tezos-node-ansible
cd tezos-node-ansible
```


And finally, just run some of the following commands depending on what network you want to execute:
``` bash
sudo ansible-playbook hangzhounet.yml
# or
sudo ansible-playbook mainnet.yml
```

## Default Variables
------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

The Tezos network you wish to provision. This variable does not have a default, so you must set it. Typically, values are `carthagenet` or `mainnet`. The `tezos_network` value is used for several purposes; naming of docker containers, naming of a docker network, selection of which Tezos network to use, and validating that snapshot imports are from the expected network

    tezos_network:

The location where on the host the Tezos nodes data directory will reside. This role uses Docker bind mounts over docker volumes.

    node_data_dir: "~/tezos/{{ tezos_network }}_node"

The location on the host where the Tezos client configuration will reside. This directory contains client configuration and keys used by the `tezos-client` command.

    client_data_dir: "~/tezos/{{ tezos_network }}_client"

The tezos docker image to use.

    tezos_docker_image: tezos/tezos:v9.4

The history mode you wish to operate your node in. Options are full, archive or snapshot (currently only tested using `full`)

    history_mode: full

Bootstrap strategy controls how your node will bootstrap. `genesis` will bootstrap without a snapshot. Specify `snapshot` to have the role download and import a snapshot.

    bootstrap_strategy: genesis

The path or URL to the snapshot file that will be used for the initial import of your node. If the value provided begins with `http://` or `https://`, the role will download a snapshot from that URL. If the provided value is a Unix file path such as `/var/tmp/a_tezos_snapshot` the role will copy the snapshot from the Ansible host machine to the target.

    snapshot_url:

The path or URL to the snapshot file that will be used for the initial import of your node. The snapshot will be downloaded to the target host's filesystem and mounted via a volume into a short-lived docker image responsible for the import process.

    snapshot_tmp_file: /tmp/snapshot


## License
-------

MIT
