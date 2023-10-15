# KeyGuard

This is meant to be a bitwarden/hashicorp vault replacement.

The goal is to implement a standard REST interface that both machines and humans can interact with. 
It should do all permissions processing server side.

Relevant Issues:  
[Hashicorp /sercret/search](https://github.com/hashicorp/vault/issues/1973)  
[Bitwarden external-secrets operator support](https://github.com/external-secrets/external-secrets/issues/2661)

## cli interface
```
keyguard (kg)
```
GET
**keyguard get/g**
```bash
keyguard g secretname
# returns all keys (not values)
keyguard g secretname.key
# returns value for key
```

POST
**keyguard update/u**
```bash
keyguard u secretname
# update all keys (if valid input)
keyguard u secretname.key
# update value for key
```

DELETE
**keyguard delete/d**
```bash
keyguard d secretname
# update entire 
keyguard d secretname.key
# update value for key
```

```bash
keyguard serve -p port
```



## Major backend design decisions:

### permissions scheme
- should we try to mirror kubernetes permissions style?
- look at kubewarden
- look at ldap
- look at how hashicorp does it
- check how google/aws do it
---

### ideas:

General data format:
key: {
    key: value
}
- top level key is the logical name for the "group" (name of entity eg. UCLA, RancherGov, ExampleApplication, A website, etc)
- subkeys are names of the keys themselves (username, password, secure note, certificate, etc)
- value is the actual value

machine accounts and user accounts:
- ?

### Data in-transit formats:
All formats should be encrypted
- default to protobuf
- yaml/json should also be supported

### Data on disk format
- encrypted protobuf

### Data in memory format
- should add optional memory encrytion as well for confidential computing (low prio)
