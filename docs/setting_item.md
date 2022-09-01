<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->


# JupyterHub Setting items

## Run

JupyterHub run by
```
jupyterhub _CONFIG_FILE_PY_
```

To generate config file in where you want to make such as `/etc/jupyterhub`
```
jupyterhub --generate-config
```

## Items

[Sample (jupyterhub_config.py)](./jupyterhub_config.py)

### IP/port

- `c.JupyterHub.ip`

	```
	c.JupyterHub.ip = '192.168.1.160'
	```


- `c.JupyterHub.port`

	```
	c.JupyterHub.port = 80
	```

- `c.JupyterHub.hub_ip`

	This is the ip address for spawner. Ordinaly it uses default (localhost)


- `c.JupyterHub.hub_port`

	This is the port for spawner. Ordinaly it uses default (localhost)

- `c.ConfigurableHTTPProxy.api_url`

	(old name : 'proxy_api_ip')

	This is the port for internal api. Ordinaly it uses default (localhost)

	```
	c.ConfigurableHTTPProxy.api_url = 'http://10.0.1.4:5432'
	```

### User

- `c.Authenticator.allowed_users`

	```
	c.Authenticator.allowed_users = {'user_01', 'user_02', 'user_03'}
	```

- `c.Authenticator.admin_users`

	Admin user is able to
	
	- add/remove allowed_users
	- stop/restart server

	When `JupyterHub.admin_access` is `True`, admin_user can control them.

	if this users contain in allowed_users, add to allow_users automatically.

	```
	c.Authenticator.admin_users = {"user_01"}
	```

	You can choice group by `c.PAMAuthenticator.admin_groups`.

### spawners

- `c.Spawner.notebook_dir`

	This directory must be exist.

	```
	c.Spawner.notebook_dir = '~/JupyterHubRoot'
	```

---
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
