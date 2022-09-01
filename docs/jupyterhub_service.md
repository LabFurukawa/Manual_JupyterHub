<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->


# JupyterHub Service

This setting is for Ubuntu (like Debian).

Ubuntu starts service by .service file from a few directories.

## 1. Create config file

1. Change directory to '/etc/systemd/system'

```
cd /etc/systemd/system
```

2. Create .service file for jupyterhub.

```
touch jupyterhub.service
```

3. Write info

[Sample (jupyterhub.service)](./jupyterhub.service)

/etc/systemd/system/jupyterhub.service

```
[Unit]
Description = JupyterHub daemon
Wants = network-online.taget
After = network-online.taget

[Service]
User = root
ExecStart = jupyterhub /etc/jupyterhub/jupyterhub_config.py
WorkingDirectory = /etc/jupyterhub/

[Install]
WantedBy = multi-user.target
```

## Activate and Start

### Activate service file

```
systemctl enable _SERVICE_FILE_NAME_
```

### Start service
```
systemctl start _SERVICE_FILE_NAME_
```

---
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
