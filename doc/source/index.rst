===================================
Barbican role for OpenStack-Ansible
===================================

This Ansible role installs and configures OpenStack barbican.

To clone or view the source code for this repository, visit the role repository
for `os_barbican <https://github.com/openstack/openstack-ansible-os_barbican>`_.

.. toctree::
   :maxdepth: 2

   configure-barbican.rst

Adding The Service to Your OpenStack-Ansible Deployment
-------------------------------------------------------

To add a new service to your OpenStack-Ansible (OSA) deployment:

* Define ``key-manager_hosts`` in your ``conf.d`` or
  ``openstack_user_config.yml``. For example:

  .. code-block:: yaml

      key-manager_hosts:
        infra1:
          ip: 172.20.236.111
        infra2:
          ip: 172.20.236.112
        infra3:
          ip: 172.20.236.113

* Create respective LXC containers (skip this step for metal deployments):

  .. code-block:: console

     openstack-ansible openstack.osa.containers_lxc_create --limit barbican_all,key-manager_hosts

* Run service deployment playbook:

  .. code-block:: console

     openstack-ansible openstack.osa.barbican

For more information, please refer to the `OpenStack-Ansible project documentation <https://docs.openstack.org/project-deploy-guide/openstack-ansible/latest/>`_.

Always verify that the integration is successful and that the service behaves
correctly before using it in a production environment.

Default variables
~~~~~~~~~~~~~~~~~

.. literalinclude:: ../../defaults/main.yml
   :language: yaml
   :start-after: under the License.

Dependencies
~~~~~~~~~~~~

This role needs pip >= 7.1 installed on the target host.

This role requires the following variables to be defined:

.. code-block:: yaml

    barbican_galera_address
    barbican_galera_password
    barbican_oslomsg_rpc_password
    barbican_service_password
    keystone_admin_user_name
    keystone_auth_admin_password
    keystone_admin_tenant_name

Example playbook
~~~~~~~~~~~~~~~~

.. literalinclude:: ../../examples/playbook.yml
   :language: yaml

Tags
~~~~

This role supports two tags: ``barbican-install`` and ``barbican-config``. The
``barbican-install`` tag can be used to install and upgrade. The ``barbican-
config`` tag can be used to maintain configuration of the service.
