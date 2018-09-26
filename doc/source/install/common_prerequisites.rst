Prerequisites
-------------

Before you install and configure the sardonic service,
you must create a database, service credentials, and API endpoints.

#. To create the database, complete these steps:

   * Use the database access client to connect to the database
     server as the ``root`` user:

     .. code-block:: console

        $ mysql -u root -p

   * Create the ``sardonic`` database:

     .. code-block:: none

        CREATE DATABASE sardonic;

   * Grant proper access to the ``sardonic`` database:

     .. code-block:: none

        GRANT ALL PRIVILEGES ON sardonic.* TO 'sardonic'@'localhost' \
          IDENTIFIED BY 'SARDONIC_DBPASS';
        GRANT ALL PRIVILEGES ON sardonic.* TO 'sardonic'@'%' \
          IDENTIFIED BY 'SARDONIC_DBPASS';

     Replace ``SARDONIC_DBPASS`` with a suitable password.

   * Exit the database access client.

     .. code-block:: none

        exit;

#. Source the ``admin`` credentials to gain access to
   admin-only CLI commands:

   .. code-block:: console

      $ . admin-openrc

#. To create the service credentials, complete these steps:

   * Create the ``sardonic`` user:

     .. code-block:: console

        $ openstack user create --domain default --password-prompt sardonic

   * Add the ``admin`` role to the ``sardonic`` user:

     .. code-block:: console

        $ openstack role add --project service --user sardonic admin

   * Create the sardonic service entities:

     .. code-block:: console

        $ openstack service create --name sardonic --description "sardonic" sardonic

#. Create the sardonic service API endpoints:

   .. code-block:: console

      $ openstack endpoint create --region RegionOne \
        sardonic public http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        sardonic internal http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        sardonic admin http://controller:XXXX/vY/%\(tenant_id\)s
