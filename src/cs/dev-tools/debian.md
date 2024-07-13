

## How to add fingerprint authentication in debian

```shell
sudo pam-auth-update
```

If there is not fingerprint authentication option, add it with 

```shell
sudo apt install fprintd libpam-fprintd
```

