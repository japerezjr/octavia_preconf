octavia_preconf
=========

This is a role for performing the pre-requisite tasks to enable amphora provider for octavia for example creating a network and a subnet for amphorae, uploading the image to glance, creating ssh keys etc. This is mainly intended for running octavia in a k8s environment

Requirements
------------

There are certain requirements for running this role
1. this role needs to be run on any of the nodes which has access to the keystone admin endpoint
2. this role also needs access to the k8s cluster as it tries to create "octavia-certs" secret in the openstack namespace to it needs access to kubectl utility

Role Variables
--------------

The available variables can be found in the defaults/main.yml file

Dependencies
------------

The role was tested with the below versions of ansible and openstacksdk:

+++\n
pip install "ansible>=2.9"  "openstacksdk>=1.0.0"
+++\n

it is preferred to create a virtual environment with python and install the dependencies there

Example Playbook
----------------

here's an example playbook:

+++
- name: Pre-requisites for enabling amphora provider in octavia
  hosts: localhost
  environment:
    OS_ENDPOINT_TYPE: internalURL
    OS_INTERFACE: internalURL
    OS_USERNAME: 'admin'
    OS_PASSWORD: 'password'
    OS_PROJECT_NAME: 'admin'
    OS_TENANT_NAME: 'admin'
    OS_AUTH_TYPE: password
    OS_AUTH_URL: 'http://keystone.openstack.svc.cluster.local/v3'
    OS_USER_DOMAIN_NAME: 'default'
    OS_PROJECT_DOMAIN_NAME: 'default'
    OS_CLOUD: 'openstack_helm'
    OS_REGION_NAME: 'RegionOne'
    OS_IDENTITY_API_VERSION: 3
    OS_AUTH_VERSION: 3
    NOVA_ENDPOINT_TYPE: internalURL
  roles:
    - /root/octavia_preconf
+++


Author Information
------------------

Punit Kundal
