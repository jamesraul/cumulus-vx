# quick start

create your links / toplogy by editing the topology.dot file then run the convertor to generate the Vagrant file. Use your
normal vagrant commands to build and access.

## create the Vagrantfile from the dot topology
    python topconvert.py topology.dot -p virtualbox

## start the VMs

    vagrant up

## connect to a device/VM

    vagrant ssh <device name>

## destroy the setup

    vagrant destroy -f

