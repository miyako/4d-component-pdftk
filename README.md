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
range|TEXT|range, qualifier, rotation
input_pw|TEXT|password

```
$path:=Get 4D folder(Current resources folder)+"sample.pdf"

C_OBJECT($params)

  //input PDF files
ARRAY OBJECT($in;2)
OB SET($in{1};"path";$path;"range";"1")
OB SET($in{2};"path";$path;"range";"1east")
OB SET ARRAY($params;"in";$in)

  //encrypt_40bit | encrypt_128bit
OB SET($params;\
"encrypt";"128bit";\
"owner_pw";"opass";\
"user_pw";"upass";\
"allow";"printing,fillin")

  //other options
OB SET($params;\
"options";"flatten,need_appearances,compress,keep_first_id,drop_xfa")

$pdf:=pdftk_cat ($params)

BLOB TO DOCUMENT(System folder(Desktop)+"cat.pdf";$pdf)
```
