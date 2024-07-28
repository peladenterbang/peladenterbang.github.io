# 🔐 Generate SSH key with putty gen

1. download putty in [https://www.putty.org/](https://www.putty.org/)
2. open puttygen (search on windows bar)

&#x20;

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

3. click generate (move mouse on the blank are to generate randomly key)

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

4. after finish generating ssh-keygen, save private key and public key.

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

5. inject public key to your remote node

```
# on linux add to 
nano .ssh/authorized_keys
```

6. access your node with private key.

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption><p>go to session > sign your username@nodeaddress and port</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption><p>go to connection > SSH > Auth > Browse your privete key > then click open</p></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
