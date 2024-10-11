# Bandit linux game

[https://overthewire.org/wargames/bandit/](https://overthewire.org/wargames/bandit/)

ssh bandit17@bandit.labs.overthewire.org -p 2220

# Soluzioni - hint
## #11
```
orig=$(echo -n {A..Z} {a..z} | tr -d ' ')
trns=$(echo -n {N..Z} {A..M} {n..z} {a..m} | tr -d " ")
cat data.txt | tr $orig $trns
```

## #12 - hexdump
```
cd es12-hexdump
g++ test.c -o test
hexdump test -C > test.hexdump
xxd -r test.hexdump
```

## #13
```
ssh bandit14@127.0.0.1 -p 2220 -i sshkey.private
```

## #14
```
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

## #15
```
openssl s_client -connect localhost:30001
<submit level 15 password>
```

## #16
(BOH)
```bash
# Find the correct port:

# 1. List all ports
nmap localhost -p 31000-32000 -Pn | grep ^[[:digit:]] | grep open | awk '{print $1}' | sed 's/\/tcp//'

# 2. Try to connect to each port and execute:
echo "currentLevelPWD" | openssl s_client -connect "localhost:31790" -ign_eof

# When you have found the port, if the password is correct, you'll be returned a private key.
# You'll need that key to access levl 17.
# Access level 17 with:
# chmod 400 passwords/17.privkey
# ssh bandit17@bandit.labs.overthewire.org -p 2220 -i passwords/17.privkey
```

