# Services

_Before checking the status of the SSH service, make sure you have the SSHD service enabled._

- #### Turning ON the SSHD service at boot time

  ```bash
  systemctl enable sshd.service
  ```

  _To turn it off at boot time, please enter `systemctl disable sshd.service`._

- #### Check if a service is enabled or disabled

  ```bash
  systemctl status sshd.service
  ```

  _It will display a message of **active** or **inactive** service._

- #### Reload SSHD configuration changes

  ```bash
  systemctl start sshd.service
  systemctl restart sshd.service
  systemctl stop sshd.service
  systemctl reload sshd.service
  ```

  _The `start` option will initiate the SSHD service, `stop` will stop it, and finally, `restart` or `reload` will refresh the new configurations_.
