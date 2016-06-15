The purpose of this role is to start inventory hosts, instanciating them first
if necessary. It will create / start any host which name ends in ``.lxc``.

Note that you need ``lxc``, ``dsnmasq``, and ``sudo`` to be properly
configured. And ``lxc-python2`` (which require ``lxc-dev``) installed in your
ansible environement. That means that you can create a container with internet
access and that you can resolve it by ``name.lxc``.

Consider this example inventory::

    [flow]
    flow.lxc lxc_template_options='-r wheezy'

    [rabbitmq]
    rabbitmq.lxc

    [redis]
    redis.lxc

And a playbook like that::

    ---

    - hosts: localhost
      become: true
      become_user: root
      become_method: sudo
      roles:
      - pdoc.boot

    - hosts: redis
      roles:
      - geerlingguy.redis

    - hosts: rabbitmq
      roles:
      - alexey.rabbitmq

First, pdoc.boot will start the containers and create them if they don't exist,
then plays will be executed normally on rabbitmq and redis container hosts.

Note that this will add to your ssh_config::

    Host *.lxc
        # No need for security for disposable test containers
        UserKnownHostsFile /dev/null
        StrictHostKeyChecking no
        User root
