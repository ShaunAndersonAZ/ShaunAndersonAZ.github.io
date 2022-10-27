---
published: true
header:
  overlay_image: #/assets/images/rocky-mtns.jpg
  caption: #"[CC License](https://creativecommons.org)"
categories:
        #- Testing
---
# Create a Key for github access
In order to push to github now you have to use a more secure method.

## Generate keypair

```
ssh-keygen -t ed25519 -C "shaunandersonaz@gmail.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/sanderson/.ssh/id_ed25519): /home/sanderson/.ssh/pc102022
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/sanderson/.ssh/pc102022
Your public key has been saved in /home/sanderson/.ssh/pc102022.pub
The key fingerprint is:
SHA256:<key fingerprint> shaunandersonaz@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
|  Random Art     |
+----[SHA256]-----+
```

Since we use a passphrase to keep things simple but secure we'll add this to the ssh-agent.

```
eval $(ssh-agent -s)
Agent pid 26288
```

Next add the key to the agent

```
ssh-add ~/.ssh/pc10202
Enter passphrase for /home/sanderson/.ssh/pc102022: 
Identity added: /home/sanderson/.ssh/pc102022 (shaunandersonaz@gmail.com)
```

Now we need to add the public key to github. Login to your account and follow the directions [here:](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

You can test your new key by attempting to ssh.

```
ssh -T git@github.com
```

Looking for this:
```
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
Hi ShaunAndersonAZ! You've successfully authenticated, but GitHub does not provide shell access.
```

Need to switch the remote URL.  Verify current setting:

```
git remote -v
origin	https://github.com/ShaunAndersonAZ/ShaunAndersonAZ.github.io.git (fetch)
origin	https://github.com/ShaunAndersonAZ/ShaunAndersonAZ.github.io.git (push)
```

Change to SSH:

```
git remote set-url origin git@github.com:ShaunAndersonAZ/ShaunAndersonAZ.github.io.git
```

Verify change:

```
git remote -v
origin	git@github.com:ShaunAndersonAZ/ShaunAndersonAZ.github.io.git (fetch)
origin	git@github.com:ShaunAndersonAZ/ShaunAndersonAZ.github.io.git (push)
```

Now attempt to push:

```
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 1.20 KiB | 1.20 MiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
```

<script src="https://utteranc.es/client.js"
        repo="shaunandersonaz/shaunandersonaz.github.io"
        issue-term="pathname"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>

