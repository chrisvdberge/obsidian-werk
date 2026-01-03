---
created: 2025-11-16T08:08
updated: 2025-11-16T08:10
tags:
  - bitbucket
---


- pipeline setup:
	- download key from service account
		- base64 encode it
			- on windows:
			  `certutil downloaded_keyfile.json encoded_key.txt`
			- on macos
			  `openssl base64 -in <infile> -out <outfile>`
		- copy the key from the encoded_key.txt file
		- add repository variable in bitbucket
		  KEY_FILE with the copied string