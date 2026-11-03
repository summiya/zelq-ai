# Deploy ZELQ AI to an existing Oracle Always Free VM

The website is **static**: `index.html` already contains HTML, CSS, JS, the selected logo and interactive project demos. No Node.js server, database, account keys, or API calls are required.

**Note:** minification makes source more compact, not secret. Browsers can still inspect frontend HTML/CSS/JS, and this GitHub repository is public.

## 1. Connect to your VM

In Oracle Cloud Console, find the VM's public IP under **Compute → Instances**. On macOS Terminal:

```sh
chmod 400 ~/Downloads/YOUR-KEY.key
ssh -i ~/Downloads/YOUR-KEY.key ubuntu@YOUR_PUBLIC_IP
```

Use `opc@` for Oracle Linux instead of `ubuntu@`.

Check OS: `cat /etc/os-release`.

## 2. Install Nginx

**Ubuntu:**

```sh
sudo apt update
sudo apt install -y nginx certbot python3-certbot-nginx
```

**Oracle Linux:**

```sh
sudo dnf install -y nginx
```

Both:

```sh
sudo systemctl enable --now nginx
sudo ss -ltnp | grep -E ':(80|443)'
```

If another service already uses port 80 or 443, preserve it and integrate the domain into your existing reverse proxy instead of stopping it.

## 3. Clone and configure

```sh
cd ~
git clone https://github.com/summiya/zelq-ai.git
sudo mkdir -p /var/www/zelq-ai
sudo install -m 0644 ~/zelq-ai/index.html /var/www/zelq-ai/index.html
sudo cp ~/zelq-ai/deploy/nginx-zelq-ai.conf /etc/nginx/conf.d/zelq-ai.conf
sudo nginx -t
sudo systemctl reload nginx
curl -I -H 'Host: zelqai.com' http://127.0.0.1/
```

Check `server_name` in the Nginx config: use the actual purchased domain if different.

If Oracle Linux SELinux denies static-file access, inspect `sudo journalctl -u nginx`, then run `sudo restorecon -Rv /var/www/zelq-ai` when appropriate.

## 4. OCI firewall/security rules

In the instance's VCN security list or Network Security Group, allow **stateful inbound TCP** from `0.0.0.0/0` to destination ports **80** and **443**. Keep SSH port 22 restricted to trusted sources where practical. Do not change WireGuard's UDP rule.

If Ubuntu UFW is **already active**, allow 80 and 443 with `sudo ufw allow 80/tcp` and `sudo ufw allow 443/tcp`. Do not enable UFW until SSH access is allowed.

If Oracle Linux firewalld is active:

```sh
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload
```

## 5. DNS

In the domain's DNS management:

| Type | Host | Value |
| --- | --- | --- |
| A | @ | YOUR_PUBLIC_IP |
| CNAME | www | zelqai.com |

Remove old/conflicting DNS records for the same host, and avoid an AAAA record unless IPv6 is configured on the VM.

Verify `dig +short zelqai.com` and `dig +short www.zelqai.com` resolve correctly.

## 6. Free HTTPS certificate

For Ubuntu, after DNS is correct and port 80 is reachable:

```sh
sudo certbot --nginx -d zelqai.com -d www.zelqai.com --redirect
sudo certbot renew --dry-run
```

For Oracle Linux, install Certbot according to the official instructions at https://certbot.eff.org/instructions?ws=nginx before running the same commands. Ensure renewal is scheduled according to those instructions.

## 7. Verify and update

```sh
curl -I https://zelqai.com/
curl -I -H 'Accept-Encoding: gzip' https://zelqai.com/
```

The home page appears at `https://zelqai.com/` **without `.html`**. Nginx serves `index.html` automatically as the default index page.

For future site changes:

```sh
cd ~/zelq-ai
git pull --ff-only origin main
sudo install -m 0644 index.html /var/www/zelq-ai/index.html
```

If Nginx says 404, check the file exists at `/var/www/zelq-ai/index.html`; if it says 403, inspect permissions/SELinux; if it times out, check OCI ingress rules and OS firewall; if Certbot errors, check DNS and reachability on TCP 80.

**Publishing GitHub changes does not automatically deploy to the Oracle VM.**
