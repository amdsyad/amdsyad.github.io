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

- Please ensure that all required fields listed below are properly added to your domain configuration.

![image](https://raw.githubusercontent.com/amdsyad/amdsyad.github.io/refs/heads/main/assets/images/MailGun.png)

- Here is a sample configuration set up such as **TXT** and **MX** record in the Advanced Domain Configuration section of a [Namecheap](https://www.namecheap.com/) domain.

![image](https://raw.githubusercontent.com/amdsyad/amdsyad.github.io/refs/heads/main/assets/images/namecheap.png)


## <span style="color:#00ff88">Mail Template Setup</span>

Here is a sample GoPhish dashboard. From this interface, you can configure key components such as the **Sending Profile**, **Email Template**, and **Landing Page**.

For the purpose of this demonstration, the focus will be on creating a custom email template. The Sending Profile can be set up separately using your SMTP mail service provider, such as Mailgun, as configured earlier. 

Here is an example of HTML code and its corresponding page rendering, designed for a phishing campaign simulation.



```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"/>
	<title>Google Drive Backup Failure</title>
</head>
<body style="margin:0; padding:0; font-family:Segoe UI, Arial, sans-serif; background-color:#f4f6f8; color:#323130;">
<table bgcolor="#f4f6f8" border="0" cellpadding="0" cellspacing="0" width="100%">
	<tbody>
		<tr>
			<td align="center" style="padding:20px;">
			<table bgcolor="#ffffff" border="0" cellpadding="0" cellspacing="0" style="border-radius:8px; box-shadow:0 2px 4px rgba(0,0,0,.1);" width="600"><!-- Logo -->
				<tbody>
					<tr>
						<td align="center" style="padding:20px; border-bottom:1px solid #e1e1e1;"><img alt="Google" src="" style="display:block;" width="120" /></td>
					</tr>
					<!-- Body -->
					<tr>
						<td style="padding:20px; font-size:14px; line-height:1.6; color:#323130;">
						<p>Dear Staff,</p>

						<p>Our system has detected that your Google Drive backup was not completed successfully. As a result, some of your files and documents may be at risk of being permanently lost.</p>

						<p>To protect your files and ensure your backup is complete, please click the link below:</p>

						<p style="text-align:center; margin:30px 0;"><a href="{{.URL}}" style="background-color:#1a73e8; color:#ffffff; padding:12px 20px; text-decoration:none; border-radius:4px; font-weight:600; font-size:14px; display:inline-block;">Complete Google Drive Backup Now </a></p>

						<p><strong>Important:</strong> If this issue is not resolved within 24 hours, your files may be deleted permanently and recovery will not be possible.</p>

						<p>Best regards,<br />
						IT Support</p>
						<img alt="" src="" style="display: none" /></td>
					</tr>
				</tbody>
			</table>
			</td>
		</tr>
	</tbody>
</table>

<p>{{.Tracker}}</p>
</body>
</html>
```
