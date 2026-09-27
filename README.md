\# Mayank Rawat — Portfolio Deployment on AWS EC2 (HTTP \& HTTPS)



Personal portfolio site deployed on an AWS EC2 instance, accessible over both \*\*HTTP (insecure)\*\* and \*\*HTTPS (secure)\*\* to demonstrate the difference in a live environment.



🔗 \*\*Live site:\*\* \[mayankrawat.duckdns.org](https://mayankrawat.duckdns.org)



\## Deployment Details



| Setting | Value |

|---|---|

| OS | Amazon Linux 2023 |

| Instance Type | t2.micro |

| Web Server | Nginx |

| Region | Mumbai (ap-south-1) |

| Domain | DuckDNS (mayankrawat.duckdns.org) |

| Security | SSH restricted, HTTPS ready |



\## Architecture



\- \*\*EC2 Instance\*\*: Amazon Linux 2023, hosting the site via Nginx

\- \*\*DuckDNS\*\*: Free dynamic DNS service mapping a domain to the EC2 public IP

\- \*\*Security Group\*\*: Controls which ports are open to the internet

\- \*\*SSL Certificate\*\*: Issued via Let's Encrypt/Certbot for the secure version



\## 1. Insecure Deployment (HTTP)



\- Accessed via `http://mayankrawat.duckdns.org`

\- Browser shows a \*\*"Not secure"\*\* warning in the address bar

\- Port 80 open in the Security Group (inbound rule: HTTP, source `0.0.0.0/0`)

\- \*\*Risk\*\*: Traffic (including any form data) travels unencrypted — visible to anyone intercepting it



\*\*Screenshot:\*\*

!\[Insecure HTTP Deployment](images/insecure-http.jpg)



\## 2. Secure Deployment (HTTPS)



\- Accessed via `https://mayankrawat.duckdns.org`

\- Browser shows a padlock — connection is encrypted and trusted

\- Port 443 open in the Security Group (inbound rule: HTTPS, source `0.0.0.0/0`)

\- SSL/TLS certificate obtained via Certbot for the DuckDNS domain

\- \*\*Benefit\*\*: Traffic is encrypted end-to-end



\*\*Screenshot:\*\*

!\[Secure HTTPS Deployment](images/secure-https.jpg)



\## Notes: HTTP vs HTTPS on EC2



| Aspect | HTTP (Insecure) | HTTPS (Secure) |

|---|---|---|

| Port | 80 | 443 |

| Encryption | None | TLS/SSL encrypted |

| Certificate needed | No | Yes |

| Browser indicator | "Not Secure" warning | Padlock icon |

| Use case | Testing/learning only | Production websites |



\*\*Key takeaways:\*\*

\- Security Groups act as a virtual firewall — only open the ports you actually need

\- Never use plain HTTP for anything handling sensitive data (logins, payments, personal info)

\- Free SSL certificates are available via Let's Encrypt (Certbot) for real domains

\- For production, it's best practice to redirect all HTTP traffic to HTTPS automatically



\## How to Reproduce



```bash

\# Install Nginx on Amazon Linux 2023

sudo dnf update -y

sudo dnf install nginx -y

sudo systemctl start nginx

sudo systemctl enable nginx



\# Point a free DuckDNS domain to your EC2 public IP

\# (sign up at duckdns.org, create a subdomain, update it to your instance's IP)



\# For HTTPS with Certbot (requires the domain to already resolve)

sudo dnf install certbot python3-certbot-nginx -y

sudo certbot --nginx -d mayankrawat.duckdns.org

```



\## Tech Stack

\- AWS EC2 (Amazon Linux 2023)

\- Nginx

\- DuckDNS (domain)

\- Let's Encrypt (Certbot) for SSL

