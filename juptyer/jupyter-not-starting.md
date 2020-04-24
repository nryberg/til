# Jupyter on Local Server

/home/nick/launch_jupyter.sh
```
Apr 13 00:06:29 littlebox launch_jupyter.sh[21824]: /home/nick/launch_jupyter.sh: line 6: jupyter: command not found
Apr 13 00:06:29 littlebox systemd[1]: jupyter.service: Main process exited, code=exited, status=127/n/a
Apr 13 00:06:29 littlebox systemd[1]: jupyter.service: Failed with result 'exit-code'.
Apr 13 00:06:39 littlebox systemd[1]: jupyter.service: Service hold-off time over, scheduling restart.
Apr 13 00:06:39 littlebox systemd[1]: jupyter.service: Scheduled restart job, restart counter is at 38345.
Apr 13 00:06:39 littlebox systemd[1]: Stopped jupyter.service.
Apr 13 00:06:39 littlebox systemd[1]: Started jupyter.service.
```

# Resolution

* Had to fix the server address from x.x.1.234 => x.x.4.234 since we're Eero'ing it
* Had to reset the password.  Required a full server reboot, and a little common sense
	* Used a passwd generator on a local instance of Jupyter.
	* Pasting the results into shell was painful until switching back to the Putty
* Updated server IP in Jupyter config file similar to above.

Works like a dream now. 
