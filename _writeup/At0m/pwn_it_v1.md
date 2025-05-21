---
layout: default
title: Pwn_it_v1
date: 2025-05-20
---

# Installation

#### Docker

- Install docker by using: sudo pacman -S docker in arch or sudo apt install docker in debain based OS.

```bash
╰─[:)] % sudo pacman -S docker
```

#### Starting Docker

```bash
╰─[:)] % sudo systemctl start docker
```

```bash
╰─[:)] % sudo systemctl enable docker
```

- First command start the docker and second command makes command start after boot automatically.

#### Pulling from docker

```bash
╰─[:)] % sudo docker pull 0x7375646f/pwn_it_v1                          
Using default tag: latest
latest: Pulling from 0x7375646f/pwn_it_v1
Digest: sha256:933a52d4b7d21e5fd93ce71400f7086780bbef19fe81df556540a8d77a46c5ca
Status: Image is up to date for 0x7375646f/pwn_it_v1:latest
docker.io/0x7375646f/pwn_it_v1:latest
```

#### Testing Program

```bash
╰─[:(] % sudo docker run -it 0x7375646f/pwn_it_v1                       
Enter username: admin
Enter password: 
Access denied!
```

- After running it we can see that it gives access denied everytime.

#### Getting Shell

```bash
╰─[:(] % sudo docker run -it --entrypoint /bin/bash 0x7375646f/pwn_it_v1
root@9aad99c650d5:/# 
```

- `--entrypoint /bin/bash`: Specifies the entrypoint for the container. Instead of running the default command for the image, it overrides it and runs `/bin/bash` (the shell) when the container starts.

#### Exploring

```bash
root@9aad99c650d5:/ ls
auth.sh  bin  boot  dev  etc  home  lib  lib.usr-is-merged  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@9aad99c650d5:/ cat auth.sh
#!/bin/bash
read -p "Enter username: " user
read -sp "Enter password: " pass
echo ""
if [[ "$user" == "MrRobot" && "$pass" == "h4cked" ]]; then
    echo "Authentication successful!"
    exec /bin/bash
else
    echo "Access denied!"
    exit 1
fi
root@9aad99c650d5:/# 
```

- So that was the program that was running as we can see the username and password was `MrRobot` and `h4cked` of before program.

```bash
root@9aad99c650d5:/ whoami  
root
root@9aad99c650d5:/ cd /root
root@9aad99c650d5:~ ls -la
total 16
drwx------ 1 root root   58 Jan 24 04:31  .
drwxr-xr-x 1 root root    0 Mar 23 16:21  ..
-rw------- 1 root root   63 Jan 24 04:31  .bash_history
-rw-r--r-- 1 root root 3106 Apr 22  2024  .bashrc
-rw-r--r-- 1 root root   81 Jan 24 04:22 '.flag?.txt'
drwxr-xr-x 1 root root   10 Jan 24 04:19  .local
-rw-r--r-- 1 root root  161 Apr 22  2024  .profile
```

- Since I am root i have all permissions, I went to `/root` directory and used `ls -la` to list all the files (even hidden) that were in that directory.
- We can see `'.flag?.txt'`

```bash
root@9aad99c650d5:~ cat '.flag?.txt'
Hm interesting thing that i dk too. Try figuring out bruh.
FQkCFR4REhYaLQMYEgIe
```

- It seems like a encrypted message, lets note it.

```bash
FQkCFR4REhYaLQMYEgIe
```

```bash
root@9aad99c650d5:~ cd /var
root@9aad99c650d5:/var ls
backups  cache  lib  local  lock  log  mail  opt  run  spool  tmp  www
root@9aad99c650d5:/var cd www
root@9aad99c650d5:/var/www ls    
html
root@9aad99c650d5:/var/www cd html
root@9aad99c650d5:/var/www/html ls
index.html
```

- I went to `/var/www/html` directory and there was a `index.html` file.

```bash
root@9aad99c650d5:/var/www/html cat index.html | head
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
  <!--
    Modified from the Debian original for Ubuntu
    Last updated: 2022-03-22
    See: https://launchpad.net/bugs/1966004
  -->
  <script>
const _0x2f4991=_0xda93;(function(_0x1d0601,_0x39d9f6){const _0x1ead35=_0xda93,_0xadfc19=_0x1d0601();while(!![]){try{const _0x4901d6=parseInt(_0x1ead35(0x9a))/0x1*(-parseInt(_0x1ead35(0x9e))/0x2)+parseInt(_0x1ead35(0xa2))/0x3*(parseInt(_0x1ead35(0x94))/0x4)+parseInt(_0x1ead35(0x9b))/0x5+-parseInt(_0x1ead35(0x93))/0x6*(parseInt(_0x1ead35(0xa1))/0x7)+parseInt(_0x1ead35(0x98))/0x8+parseInt(_0x1ead35(0x95))/0x9*(-parseInt(_0x1ead35(0xa0))/0xa)+parseInt(_0x1ead35(0x9f))/0xb;if(_0x4901d6===_0x39d9f6)break;else _0xadfc19['push'](_0xadfc19['shift']());}catch(_0x40e265){_0xadfc19['push'](_0xadfc19['shift']());}}}(_0x2c1b,0x31c70));function _0x2c1b(){const _0x21f031=['54gtRCwl','62156svkzYZ','135IzweGB','length','secret','66616jEDToV','charCodeAt','1052pdFxYA','1337615XeHUMx','fromCharCode','heregoesyoursecret','210izgAhV','3161235SqXoEW','78920cKXHnz','149849KcHRic','12BFlisG','log'];_0x2c1b=function(){return _0x21f031;};return _0x2c1b();}function xorEncryptDecrypt(_0x2163d6,_0x2a5337){const _0x22ffae=_0xda93;let _0x256bda='';for(let _0x4c4d57=0x0;_0x4c4d57<_0x2163d6[_0x22ffae(0x96)];_0x4c4d57++){_0x256bda+=String[_0x22ffae(0x9c)](_0x2163d6[_0x22ffae(0x99)](_0x4c4d57)^_0x2a5337[_0x22ffae(0x99)](_0x4c4d57%_0x2a5337[_0x22ffae(0x96)]));}return _0x256bda;}function _0xda93(_0x208bc9,_0x130d3e){const _0x2c1bd3=_0x2c1b();return _0xda93=function(_0xda935c,_0xcc38eb){_0xda935c=_0xda935c-0x92;let _0x125462=_0x2c1bd3[_0xda935c];return _0x125462;},_0xda93(_0x208bc9,_0x130d3e);}const key=_0x2f4991(0x97),encrypted=_0x2f4991(0x9d),decrypted=xorEncryptDecrypt(atob(encrypted),key);console[_0x2f4991(0x92)]('Decrypted:',decrypted);
</script>
```

- I used command `cat index.html | head`. `cat` is used to view the content while i used `|` symbol to pipe or use two commands together and i used `head` command to see only top of few content of that file since full file has too much code.
- That code starting from `<script>` seems like a obfuscated javascript code.
- We can decode it by going online in obfuscated decoder.
- I used this site [Unpacker](https://matthewfl.com/unPacker.html)
- After putting our code this there in site:

```js
const _0x2f4991=_0xda93;(function(_0x1d0601,_0x39d9f6){const _0x1ead35=_0xda93,_0xadfc19=_0x1d0601();while(!![]){try{const _0x4901d6=parseInt(_0x1ead35(0x9a))/0x1*(-parseInt(_0x1ead35(0x9e))/0x2)+parseInt(_0x1ead35(0xa2))/0x3*(parseInt(_0x1ead35(0x94))/0x4)+parseInt(_0x1ead35(0x9b))/0x5+-parseInt(_0x1ead35(0x93))/0x6*(parseInt(_0x1ead35(0xa1))/0x7)+parseInt(_0x1ead35(0x98))/0x8+parseInt(_0x1ead35(0x95))/0x9*(-parseInt(_0x1ead35(0xa0))/0xa)+parseInt(_0x1ead35(0x9f))/0xb;if(_0x4901d6===_0x39d9f6)break;else _0xadfc19['push'](_0xadfc19['shift']());}catch(_0x40e265){_0xadfc19['push'](_0xadfc19['shift']());}}}(_0x2c1b,0x31c70));function _0x2c1b(){const _0x21f031=['54gtRCwl','62156svkzYZ','135IzweGB','length','secret','66616jEDToV','charCodeAt','1052pdFxYA','1337615XeHUMx','fromCharCode','heregoesyoursecret','210izgAhV','3161235SqXoEW','78920cKXHnz','149849KcHRic','12BFlisG','log'];_0x2c1b=function(){return _0x21f031;};return _0x2c1b();}function xorEncryptDecrypt(_0x2163d6,_0x2a5337){const _0x22ffae=_0xda93;let _0x256bda='';for(let _0x4c4d57=0x0;_0x4c4d57<_0x2163d6[_0x22ffae(0x96)];_0x4c4d57++){_0x256bda+=String[_0x22ffae(0x9c)](_0x2163d6[_0x22ffae(0x99)](_0x4c4d57)^_0x2a5337[_0x22ffae(0x99)](_0x4c4d57%_0x2a5337[_0x22ffae(0x96)]));}return _0x256bda;}function _0xda93(_0x208bc9,_0x130d3e){const _0x2c1bd3=_0x2c1b();return _0xda93=function(_0xda935c,_0xcc38eb){_0xda935c=_0xda935c-0x92;let _0x125462=_0x2c1bd3[_0xda935c];return _0x125462;},_0xda93(_0x208bc9,_0x130d3e);}const key=_0x2f4991(0x97),encrypted=_0x2f4991(0x9d),decrypted=xorEncryptDecrypt(atob(encrypted),key);console[_0x2f4991(0x92)]('Decrypted:',decrypted);
```

- After putting this we get:

```js
const _0x2f4991=_0xda93;
(function(_0x1d0601,_0x39d9f6)
	{
	const _0x1ead35=_0xda93,_0xadfc19=_0x1d0601();
	while(!![])
		{
		try
			{
			const _0x4901d6=parseInt(_0x1ead35(0x9a))/0x1*(-parseInt(_0x1ead35(0x9e))/0x2)+parseInt(_0x1ead35(0xa2))/0x3*(parseInt(_0x1ead35(0x94))/0x4)+parseInt(_0x1ead35(0x9b))/0x5+-parseInt(_0x1ead35(0x93))/0x6*(parseInt(_0x1ead35(0xa1))/0x7)+parseInt(_0x1ead35(0x98))/0x8+parseInt(_0x1ead35(0x95))/0x9*(-parseInt(_0x1ead35(0xa0))/0xa)+parseInt(_0x1ead35(0x9f))/0xb;
			if(_0x4901d6===_0x39d9f6)break;
			else _0xadfc19['push'](_0xadfc19['shift']());
		}
		catch(_0x40e265)
			{
			_0xadfc19['push'](_0xadfc19['shift']());
		}
	}
}
(_0x2c1b,0x31c70));
function _0x2c1b()
	{
	const _0x21f031=['54gtRCwl','62156svkzYZ','135IzweGB','length','secret','66616jEDToV','charCodeAt','1052pdFxYA','1337615XeHUMx','fromCharCode','heregoesyoursecret','210izgAhV','3161235SqXoEW','78920cKXHnz','149849KcHRic','12BFlisG','log'];
	_0x2c1b=function()
		{
		return _0x21f031;
	};
	return _0x2c1b();
}
function xorEncryptDecrypt(_0x2163d6,_0x2a5337)
	{
	const _0x22ffae=_0xda93;
	let _0x256bda='';
	for(let _0x4c4d57=0x0;
	_0x4c4d57<_0x2163d6[_0x22ffae(0x96)];
	_0x4c4d57++)
		{
		_0x256bda+=String[_0x22ffae(0x9c)](_0x2163d6[_0x22ffae(0x99)](_0x4c4d57)^_0x2a5337[_0x22ffae(0x99)](_0x4c4d57%_0x2a5337[_0x22ffae(0x96)]));
	}
	return _0x256bda;
}
function _0xda93(_0x208bc9,_0x130d3e)
	{
	const _0x2c1bd3=_0x2c1b();
	return _0xda93=function(_0xda935c,_0xcc38eb)
		{
		_0xda935c=_0xda935c-0x92;
		let _0x125462=_0x2c1bd3[_0xda935c];
		return _0x125462;
	}
	,_0xda93(_0x208bc9,_0x130d3e);
}
const key=_0x2f4991(0x97),encrypted=_0x2f4991(0x9d),decrypted=xorEncryptDecrypt(atob(encrypted),key);
console[_0x2f4991(0x92)]('Decrypted:',decrypted);
```

- It still looks scary so lets add comments and change hex to strings.

```js
// Helper function to retrieve values from the string array
function _0x2c1b() {
    const _0x21f031 = [
        '54gtRCwl', '62156svkzYZ', '135IzweGB', 'length', 'secret', '66616jEDToV', 
        'charCodeAt', '1052pdFxYA', '1337615XeHUMx', 'fromCharCode', 'heregoesyoursecret', 
        '210izgAhV', '3161235SqXoEW', '78920cKXHnz', '149849KcHRic', '12BFlisG', 'log'
    ];
    _0x2c1b = function() {
        return _0x21f031;
    };
    return _0x2c1b();
}

// Function to map hexadecimal indices to strings
function _0xda93(index, _) {
    const _0x2c1bd3 = _0x2c1b();
    return _0xda93 = function(adjustedIndex, _) {
        adjustedIndex = adjustedIndex - 0x92; // Adjust the index
        return _0x2c1bd3[adjustedIndex];
    }, _0xda93(index, _);
}

// XOR encryption/decryption function
function xorEncryptDecrypt(data, key) {
    let decrypted = '';
    for (let i = 0; i < data.length; i++) {
        decrypted += String.fromCharCode(data.charCodeAt(i) ^ key.charCodeAt(i % key.length));
    }
    return decrypted;
}

// Retrieve the key and encrypted message
const key = _0xda93(0x97); // 'secret'
const encrypted = _0xda93(0x9d); // 'FQkCFR4REhYaLQMYEgIe'

// Decode the base64-encoded encrypted message
const decodedEncrypted = atob(encrypted);

// Decrypt the message using the XOR function
const decrypted = xorEncryptDecrypt(decodedEncrypted, key);

// Output the decrypted message
console.log('Decrypted:', decrypted);
```

- It uses XOR operation for obfuscation.
- Remember it `FQkCFR4REhYaLQMYEgIe` Its the encrypted message and `secret` is the key
- So we can write a simple python script to do convert above JS code to convert to python code to decrypt. 
- You can use [Deepseek](https://chat.deepseek.com/) for it.

```python
import base64

# Constants and helper functions
def _0x2c1b():
    return ['54gtRCwl', '62156svkzYZ', '135IzweGB', 'length', 'secret', '66616jEDToV', 'charCodeAt', '1052pdFxYA', '1337615XeHUMx', 'fromCharCode', 'heregoesyoursecret', '210izgAhV', '3161235SqXoEW', '78920cKXHnz', '149849KcHRic', '12BFlisG', 'log']

def _0xda93(index, _):
    _0x2c1bd3 = _0x2c1b()
    return _0x2c1bd3[index - 0x92]

# XOR encryption/decryption function
def xor_encrypt_decrypt(data, key):
    decrypted = ''
    for i in range(len(data)):
        decrypted += chr(ord(data[i]) ^ ord(key[i % len(key)]))
    return decrypted

# Main execution
key = _0xda93(0x97, None)  # 'secret'
encrypted = _0xda93(0x9d, None)  # 'heregoesyoursecret'

# Decode the base64 encoded encrypted string
encrypted_decoded = base64.b64decode(encrypted).decode('utf-8')

# Decrypt the data
decrypted = xor_encrypt_decrypt(encrypted_decoded, key)

# Output the decrypted data
print('Decrypted:', decrypted)
```

#### Getting Flag

```bash
╰─[:)] % python3 main.py
Decrypted: flag{easy_flag}
```

- When we run the python script we get flag `flag{easy_flag}`

#### Author: At0m

---

