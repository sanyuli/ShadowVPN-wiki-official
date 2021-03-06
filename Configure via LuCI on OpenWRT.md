If the default `client_up.sh` and `client_down.sh` won't work on your OpenWRT router,
and you couldn't figure out why, use LuCI to configure instead.

1. Clear the content of `client_up.sh` and `client_down.sh` so that
they won't change route table any more. Remove `/etc/hotplug.d/iface/30-shadowvpn` if it exists.
Then start ShadowVPN.

2. Add a new interface named `tun`, select `tun0`.

   ![image](https://cloud.githubusercontent.com/assets/1073082/4519784/4b303254-4ccb-11e4-8c93-65b193612104.png)

3. Disable `Use default gateway` of wan.

   ![image](https://cloud.githubusercontent.com/assets/1073082/4519789/7a262276-4ccb-11e4-846e-85f31584b1d0.png)

4. Add a new zone called tun. Add `interface tun` to `tun zone`. And update forward rules: `lan => tun`, `tun => wan`.

   ![image](https://cloud.githubusercontent.com/assets/1073082/4519773/fccd4138-4cca-11e4-945b-b1da19e63c92.png)

5. Add two static routes

   ![image](https://cloud.githubusercontent.com/assets/1073082/4519796/b98a5edc-4ccb-11e4-8fbc-ceccd14c35fc.png)

   If your wan is pppoe, you only need to specify the interface wan in the first rule. If your wan is static IP or DHCP, you also have to specify gateway IP.

6. (Optional) Add [chnroutes script](https://github.com/clowwindy/ShadowVPN/blob/master/samples/chnroutes.sh).
   Save it to `/etc/shadowvpn/chnroutes.sh`. Then

        chmod +x /etc/shadowvpn/chnroutes.sh

   Create `/etc/hotplug.d/iface/35-chnroutes`

        #!/bin/sh
        [ ifup = "$ACTION" ] && {
          [ wan = "$INTERFACE" ] && {
             /etc/shadowvpn/chnroutes.sh
          }
        }

7. Save and apply. Then:

        /etc/init.d/network restart

To disable ShadowVPN, go to step 5 and change default route 0.0.0.0 from tun to wan.