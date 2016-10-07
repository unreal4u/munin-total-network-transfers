# munin-total-network-transfers
Displays the total bytes transferred of machine since last boot, I use it for my Linux home server/router. The actual read is done from the following path:

`/sys/class/net/**/statistics/*x_bytes`

AFAIK, this path is the same on any Linux-based system. If it ain't, feel free to make an issue so that this path can be configured with a environment variable instead.

## How to install

- Copy the plugins to the plugins directory. On a CentOS system, this is typically `/usr/share/munin/plugins/`. Don't forget to make the symlink in `/etc/munin/plugins/`.
- Restart your munin node in order to let it know about the new plugin(s): `systemctl restart munin-node`. On other systems, `service munin-node restart` can also do the job.

## SELinux permissions

Disabling SELinux is a **bad** idea. The permissions for the plugins can be set by executing:

<pre>
chcon -h system_u:object_r:unconfined_munin_plugin_exec_t:s0 /usr/share/munin/plugins/total_network_usage
</pre>

Check your `/var/log/audit/audit.log` file in case of problems.

## TODO list

- Enable direction in graph (as the standard defined per http://munin-monitoring.org/wiki/HowToWritePlugins)
