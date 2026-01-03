---
created: 2025-12-29T12:40
updated: 2025-12-29T12:43
tags:
  - git
---

- `git clone git@github.com-company: ....
- `~/.ssh/config` contains:
  ```
  	  christianvandenberge@Mac-C02D40XQP3YW dbt % cat ~/.ssh/config
			  Host *
			  UseKeychain yes
			  
			  Host github.com-personal
			  	HostName github.com
			  	AddKeysToAgent yes
			  	UseKeychain yes
			  	IdentityFile ~/.ssh/id_ed25519
			  
			  Host github.com-company
			  	HostName github.com
			  	IdentityFile ~/.ssh/github-company
  ```
