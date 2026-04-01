---
title: Phishing Server Setup
date: 2026-03-29
categories: [Phishing]
tags: [Scam, Email phishing, Gophish, Mailserver]
---

## Introduction
Hey folks, I’m going to walk you through how to set up a phishing simulation server using GoPhish along with a mail server.

This setup is designed to help red teamers deploy and manage phishing campaigns effectively using GoPhish integrated with a fully configured mail server, including domain and server setup.

## <span style="color:#00ff88">GoPhish</span>

First, download the GoPhish release package from the official GitHub repository [GoPhish](https://github.com/gophish/gophish/releases)
Once the download is complete, extract the contents of the ZIP file to your server.

![image](https://raw.githubusercontent.com/amdsyad/amdsyad.github.io/refs/heads/main/assets/images/unzip%20the%20file.png)

1. After extracting the files, ensure the GoPhish binary has the appropriate execution permissions by applying the `chmod` command.
```bash
   chmod +x gophish
```
2. Update the `config.json` file according to your environment. For now, modify the `listen_url` parameter as shown below.
```bash
root@ubuntu-s-1vcpu-512mb-10gb-sgp1-01:/opt/gophish# cat config.json
{
        "admin_server": {
                "listen_url": "0.0.0.0:3333",
                "use_tls": true,
                "cert_path": "gophish_admin.crt",
                "key_path": "gophish_admin.key",
                "trusted_origins": []
        },
        "phish_server": {
                "listen_url": "0.0.0.0:80",
                "use_tls": false,
                "cert_path": "example.crt",
                "key_path": "example.key"
        },
        "db_name": "sqlite3",
        "db_path": "gophish.db",
        "migrations_prefix": "db/db_",
        "contact_address": "",
        "logging": {
                "filename": "",
                "level": ""
        }
}
```


3. Run the GoPhish binary. From the application logs, you will be able to retrieve the default username and password required to access the GoPhish dashboard.

```bash
root@ubuntu-s-1vcpu-512mb-10gb-sgp1-01:/opt/gophish# ./gophish
```

## <span style="color:#00ff88">MailServer</span>
[Mailgun](https://www.mailgun.com/) is integrated as the email delivery service to send phishing emails..

Here few step need to verified throught Mailgun before using the service

- Please ensure that all required fields listed below are properly added to your domain configuration. This includes records such as **TXT** and **MX**, which can typically be found under the Advanced Domain Configuration section.

![image](https://raw.githubusercontent.com/amdsyad/amdsyad.github.io/refs/heads/main/assets/images/MailGun.png)

- Here is a sample configuration set up in the Advanced Domain Configuration section of a [Namecheap](https://www.namecheap.com/) domain.

![image](https://raw.githubusercontent.com/amdsyad/amdsyad.github.io/refs/heads/main/assets/images/namecheap.png)
