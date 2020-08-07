# 4d-component-pdftk
4D component of [pdftk](https://www.pdflabs.com/tools/pdftk-server/)

updated for El Capitan:

c.f
* http://stackoverflow.com/questions/32505951/pdftk-server-on-os-x-10-11
* https://qiita.com/keitasumiya/items/83756caf2865291707fb



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
options|TEXT|combination of ``flatten``, ``need_appearances``, ``compress``, ``uncompress``, ``keep_first_id``, ``keep_final_id``, ``drop_xfa``

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

```
pdf:=pdftk_fill_form (params;fdf)
```

param|type|description
------------|------------|----
params|OBJECT|see below
fdf|BLOB|``fdf`` or ``xfdf``
pdf|BLOB|result

* properties for ``params``

property|type|description
------------|------------|----
path|TEXT|file path
input_pw|TEXT|password
options|TEXT|combination of ``flatten``, ``need_appearances``

* The components has helper functions to construct ``fdf`` or ``xfdf``

Both are Unicode aware, but it seems the filled form values on Mac Preview only appear when the user clicks the field (or re-saves the document as PDF).

* pdftk_make_fdf

```
C_OBJECT($params)

ARRAY OBJECT($fields;3)
OB SET($fields{1};"name";"Name_Last";"value";"miyako")
OB SET($fields{2};"name";"Name_First";"value";"keisuke")
OB SET ARRAY($params;"fields";$fields)

$fdf:=pdftk_make_fdf ($params)

$pdf:=pdftk_fill_form ($params;$fdf)
$path:=System folder(Desktop)+"fill_form.pdf"
BLOB TO DOCUMENT($path;$pdf)
```

* pdftk_make_xfdf

```
C_OBJECT($params)

ARRAY OBJECT($fields;3)
OB SET($fields{1};"name";"Name_Last";"value";"miyako")
OB SET($fields{2};"name";"Name_First";"value";"keisuke")
OB SET ARRAY($params;"fields";$fields)

$fdf:=pdftk_make_xfdf ($params)

$pdf:=pdftk_fill_form ($params;$fdf)
$path:=System folder(Desktop)+"fill_form.pdf"
BLOB TO DOCUMENT($path;$pdf)
```

