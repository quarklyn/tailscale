<h1 align="center">Renscale</h1>
<h2 align="center">Easily spin up an ephemeral VPN on Render using Tailscale under the hood</h2><br>

### Disclaimer:
<code>Neither me nor this project shall be in any way held responsible if your account gets banned. It is your sole responsibility to use this project in whatever way you may want. To ensure fair and sustainable access for all, please refrain from excessive usage of these services.</code><br>
### Prerequisites:
- Free [Render](https://render.com/) account.
- Free [Tailscale](https://tailscale.com/) account.<br>
### Pre Deployment Guide:
1. Signup on [Tailscale](https://login.tailscale.com/start).

    ![1](/assets/1.png)
    ![2](/assets/2.png)
2. Connect at least one device following the Tailscale introduction guide.

    ![3](/assets/3.png)
3. Go to the **Access Controls** tab and save the following JSON into **Edit file** section, replacing <code>quarklyn@github</code>
with an appropriate value from the **Users** tab.
    ```json
    {
        "acls": [
          { "action": "accept", "src": ["*"], "dst": ["*:*"] },
        ],
        "tagOwners": {
          "tag:vpn": ["quarklyn@github"],
        },
        "autoApprovers": {
          "exitNode": ["tag:vpn"],
        }
    }
    ```

    ![4](/assets/4.png)
    ![7](/assets/7.png)
4. Go to the **Keys** section in the **Settings** tab and generate an **auth key**. Paste this key into heroku when asked for.
Also save it for future use.

    ![5](/assets/5.png)
    ![6](/assets/6.png)<br>
### Deployment:
[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)<br>
### Post Deployment guide:
1. Open tailscale client on the device you want to use VPN. (Guide shows for android)

    ![A](/assets/A.jpeg)
2. Connect your client to tailscale.
3. Tap **Use exit node** and select the correct online machine after checking in tailscale [dashboard](https://login.tailscale.com/admin/machines)

    ![B](/assets/B.jpeg)
    ![C](/assets/C.jpeg)
4. VPN should start working.

    ![D](/assets/D.jpeg)<br>
### Notes:
- Make sure, you have followed the steps as precisely as possible.
- As always, heroku dynos will sleep after a certain amount of time. This repo has no hardcoded way to circumvent that (who needs a VPN 24/7 anyways ?) but it does serve a site which you can ping. So, it is totally upto YOU how you want to keep it running. Few utilities worth noting are: 
  - https://kaffeine.herokuapp.com/
  - https://cron-job.org/en/
- Each time your heroku app restarts, a new machine will pop up in tailscale dashboard and the old offline ones will disappear eventually. YOU have to make sure to choose the correct exit node each time, failing which will block your internet.
- **[Tailscale](https://tailscale.com/)** is a great tool in itself with extensive documention, make sure to try it.<br>
### Todo:
- V2 with native wireguard implementation. (iff possible)
- Support for VPN on github-actions.<br>
### Contact:
- [Telegram](https://t.me/mishizu)