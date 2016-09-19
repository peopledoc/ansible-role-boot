Basic role to ensure an SSH agent works on the client.

It ensures that a ~/.ssh directory exists and that it has the right
permissions, so should the key files, and that an ssh agent is started. It may
also add insecurity for some hosts in ~/.ssh/config.

Example usage::

    ---

    - hosts: localhost
      roles:
      - role: novafloss.boot-base
        ssh_insecure: ['*.lxc']

This will:

- ensure a default ssh key exists,
- ensure ssh config dir have the right permissions,
- ensure ssh config have the right permissions,
- ensure ssh keys have the right permissions,
- ensure an ssh agent is started and ``$SSH_AUTH_SOCK`` is defined,
- enable insecure connection to ``*.lxc`` (or any host you add to
  ``ssh_insecure``).

This role can be used prior to novafloss.boot-* roles.
