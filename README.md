# DNS-Server-Project



<img width="1188" height="552" alt="image" src="https://github.com/user-attachments/assets/215af137-a7a9-4089-a9ed-4c788017abef" />

---------------------------------------------------------------------------------------------
<img width="974" height="608" alt="image" src="https://github.com/user-attachments/assets/34ec8573-9a3a-44d0-8b99-42b7d67b88be" />
-------------------------------------------------------------------------------------

payal@LAPTOP-4S37KAPD:~$ nslookup www.mydnsproject.local localhost
Server:         localhost
Address:        127.0.0.1#53

Name:   www.mydnsproject.local
Address: 127.0.0.1

<img width="998" height="797" alt="image" src="https://github.com/user-attachments/assets/72da3314-cdf3-463f-8c74-2d2dcfd5965a" />






  -----------------------------------------
  

# DNS Server Project – One Page Full Steps

## Project Name: DNS Server Project using BIND9

### Objective:

Build a DNS system to understand how name resolution works using authoritative DNS server, recursive resolver, DNS records, TTL, and caching.

---

## Step 1: Install Required Packages

```bash
sudo apt update
sudo apt install bind9 bind9utils bind9-doc dnsutils -y
```

Check version:

```bash
named -v
```

---

## Step 2: Configure Local DNS Zone

Open file:

```bash
sudo nano /etc/bind/named.conf.local
```

Add:

```conf
zone "mydnsproject.local" {
    type master;
    file "/etc/bind/db.mydnsproject.local";
};
```

Save:
CTRL + O → Enter → CTRL + X

---

## Step 3: Create Zone File

```bash
sudo cp /etc/bind/db.local /etc/bind/db.mydnsproject.local
sudo nano /etc/bind/db.mydnsproject.local
```

Paste:

```conf
$TTL 604800

@   IN  SOA ns1.mydnsproject.local. admin.mydnsproject.local. (
        3
        604800
        86400
        2419200
        604800
)

@       IN      NS      ns1.mydnsproject.local.

ns1     IN      A       127.0.0.1
www     IN      A       127.0.0.1
app     IN      A       127.0.0.1
mail    IN      A       127.0.0.1
ftp     IN      A       127.0.0.1
api     IN      A       127.0.0.1
```

Save and exit.

---

## Step 4: Validate Configuration

Check syntax:

```bash
sudo named-checkconf
```

Check zone:

```bash
sudo named-checkzone mydnsproject.local /etc/bind/db.mydnsproject.local
```

Expected Output:

```text
OK
```

---

## Step 5: Restart DNS Service

```bash
sudo systemctl restart bind9
sudo systemctl status bind9
```

Expected:

```text
active (running)
```

---

## Step 6: Test DNS Resolution

```bash
dig @localhost www.mydnsproject.local
```

OR

```bash
nslookup www.mydnsproject.local localhost
```

Expected:

```text
127.0.0.1
```

Meaning:

```text
www.mydnsproject.local → 127.0.0.1
```

---

## Step 7: Test Recursive DNS

```bash
dig google.com
```

This shows internet DNS resolution and recursive query behavior.

---

## Step 8: Understand DNS Cache

Run again:

```bash
dig google.com
```

Second query is faster because of DNS caching and TTL.

---

## Step 9: Debug Commands

```bash
sudo systemctl status bind9
sudo journalctl -xe
sudo named-checkconf
sudo named-checkzone mydnsproject.local /etc/bind/db.mydnsproject.local
```

---

## Interview Explanation

“I built a DNS server using BIND9 where I configured an authoritative DNS zone, created A and NS records, tested resolution using dig and nslookup, and verified recursive resolution, TTL, and caching behavior.”

---

## Final Result

DNS successfully resolves:

```text
www.mydnsproject.local → 127.0.0.1
```

Project Completed Successfully.












-----------------------------------






