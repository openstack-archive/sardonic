2. Edit the ``/etc/sardonic/sardonic.conf`` file and complete the following
   actions:

   * In the ``[database]`` section, configure database access:

     .. code-block:: ini

        [database]
        ...
        connection = mysql+pymysql://sardonic:SARDONIC_DBPASS@controller/sardonic
