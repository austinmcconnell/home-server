# Pi-hole

Run Pi-hole image from [Docker Hub](https://hub.docker.com/r/pihole/pihole)

## Admin Password

One option is to set the `WEBPASSWORD` environment variable in a .env file.

Another option is to let the container generate a password on startup. If you do that, run
`docker logs pihole | grep random` to find the generated password.

## Upgrading

According to the [Official upgrade documentation](https://github.com/pi-hole/docker-pi-hole?tab=readme-ov-file#upgrading--reconfiguring),
do not run `pihole -up` or `pihole -r` to attempt to upgrade.

Instead, first read the release notes. Then update the image tag and download the image

```shell
docker pull pihole
```

 and then start the new version with

 ```shell
 docker compose up -d
 ```

> :warning: When removing your pihole container, you may be stuck without DNS until the new
> container starts. Recommend always having a fallback DNS server configured in DHCP to avoid
> potential interruptions :warning:

## Admin UI

The admin UI can be found at <https://192.168.1.20/admin>

## DNS Blocklists

Login to the admin UI. Click AdLists on the sidebar. Then manually add the following blocklists
from [hagezi/dns-blocklists](https://github.com/hagezi/dns-blocklists)

- [Multi Pro](https://github.com/hagezi/dns-blocklists?tab=readme-ov-file#pro)
  - Big broom - Cleans the Internet and protects your privacy! Blocks Ads, Affiliate, Tracking,
  Metrics, Telemetry, Phishing, Malware, Scam, Fake, Coins and other "Crap"
- [Threat Intelligence Feeds](https://github.com/hagezi/dns-blocklists?tab=readme-ov-file#tif)
  - A blocklist for blocking malware, cryptojacking, scam, spam and phishing. Blocks domains known
  to spread malware, launch phishing attacks and host command-and-control servers.
- [Anti Piracy](https://github.com/hagezi/dns-blocklists?tab=readme-ov-file#piracy)
  - Blocks websites and services that are mainly used for illegal distribution of copyrighted content

## Hostnames In Dashboard

If you are not using pihole as a DHCP server, you'll only see the IP addresses of clients in
dashboards and lists.

If you want to see the hostnames of clients, go to Settings --> DNS --> Conditional forwarding
and set `Local network in CIDR notation` and `IP address of your DHCP server (router)`.

Example

![dns conditional forwarding example](/img/pihole-dns-conditional-forwarding.png)
