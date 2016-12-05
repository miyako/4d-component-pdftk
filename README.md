# 4d-component-pdftk
4D component of [pdftk](https://www.pdflabs.com/tools/pdftk-server/)

updated to `` 2.02`` for El Capitan see http://stackoverflow.com/questions/32505951/pdftk-server-on-os-x-10-11

Examples
---

```
pdf:=pdftk_cat (params)
```

param|type|description
------------|------------|----
params|OBJECT|see below
pdf|BLOB|result

* properties for ``params``

property|type|description
------------|------------|----
in|ARRAY OBJECT|see below
encrypt|TEXT|``40bit`` or ``128bit`` (default)
owner_pw|TEXT|owner password
user_pw|TEXT|user password
allow|TEXT|combination of ``printing``, ``degradedprinting``, ``modifycontents``, ``assembly``, ``copycontents``, ``screenreaders``, ``modifyannotations``, ``fillin``, ``allfeatures``

* properties for ``in``

property|type|description
------------|------------|----
path|TEXT|file path
range|TEXT|range
input_pw|TEXT|password
