# Tailscale on OpenWRT

1. Extract the contents of root to your filesystem root using:
```
tar x -zvf tailscale-enabler-<version>.tgz -C /
```

2. Install the prerequisites for wget and tailscale using:
```
opkg update
opkg install libustream-openssl ca-bundle kmod-tun
```

3. Run tailscale for the first time:
```
/etc/init.d/tailscale start
tailscale up --accept-dns=false --advertise-routes=10.0.0.0/24
```

Both of these commands download the tailscale package to get the binaries to /tmp
The /etc/init.d/tailscale will start the tailscale daemon. 
The next command uses the tailscale CLI to configure the login and add some settings to prevent dns changes and advertise routes. Use the URL printed to login to tailscale.

4. Enable tailscale at boot:
```
/etc/init.d/tailscale enable
```

Verify by looking for an entry here:
```
ls /etc/rc.d/S*tailscale*
```

5. Reboot the router and verify that it shows up online on the [Tailscale Admin portal](https://login.tailscale.com/admin/machines).

6. To update the version of tailscale, grab the latest version [here](https://pkgs.tailscale.com/stable/#static) of the form `1.2.10_mips` and replace the same in /usr/bin/tailscale_enabler: `version="1.2.10_mips"`.
