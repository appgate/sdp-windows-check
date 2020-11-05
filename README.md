# Overview
This tool is used to be run on Windows (32bit exe). It provides various Windows related actions plus some other features. 

Note, even this tool has been initially created during the epoch of Appgate Classic, there might be some use of it still. 
But basically, when it comes to Windows related instrumenting, then you should use `wmic` [or the provided wmic wrapper](https://github.com/appgate/sdp-wmicprovider).  

## Binary
See the [latest release](https://github.com/appgate/sdp-windows-check/releases/latest) for download.

## Example of commands
You can download the binary and run to get the following usage help:
``` 
$ ./devicecheck.exe
Usage: C:\Users\raymond\source\repos\appgate-cre\extension-client-check\agc\Release\devicecheck.exe [-d]
  -fileexists <file>
  -filesizeis <file> <size>
  -filesizelarger <file> <size>
  -filesizesmaller <file> <size>
  -fileversion <file>
  -productversion <file>
  -md5sum <file>
  -sha1sum <file>
  -sha256sum <file>
  -sha384sum <file>
  -sha512sum <file>
  -regexists <root> <key> [<value>]
  -regprint <root> <key> [<value>]
  -regdatenewer <days> <pattern> <root> <key> [<value>]
    where <pattern> can contain %Y, %m and %d
  -getprivateprofilestring <appname> <key> <def> <file>
  -isavok
  -isfwok
  -isspyok
  -wscstatus <providermask>
  -fsecureavversion print | <max age in days>
  -sophosmaxage <rtime>
    where <rtime> is of the form nn['d'|'h'|'m'].
  -mcafeenewerthan print | <max age in days>
  -process <name>
  -exec <command> ...
  -isadmin
  -iscomputermemberofdomain
  -issvcrunning <name>
  -querysvc <name>
  -isportbusy <port>
  -matchoutput <cmd> <needle1> ...
  -isnetbtenabled
  -isunitmounted <driveletter>
  -deviceserialno <logicaldrive>
  -listmacaddresses
  -writecred <target> <user> <pass>
  -deletecred <target> <user>
  -downloadto <url> [-hash <hash>] <file>
    <hash> is of the form {md5,sha1,sha256,sha384,sha512}:XXXXX...
  -downloadandrun <url> [<hash>]
    <hash> is of the form {md5,sha1,sha256,sha384,sha512}:XXXXX...
  -downloadandrunasarg <url> [-hash <hash>] <cmd>
    <hash> is of the form {md5,sha1,sha256,sha384,sha512}:XXXXX...
    <cmd> may contain #f which will be expanded to the file name
      of the downloaded copy of the file to which the url points.
  -downloadanddo <url> <op> [<hash>]
    where <op> is one of: edit, explore, find, open or print
    and <hash> is of the form {md5,sha1,sha256,sha384,sha512}:XXXXX...
  -afiledateis <file> <date>
  -afiledatenewer <file> <date>
  -afiledateolder <file> <date>
    where <date> is of the form yyyymmdd[hh[mm[ss]]].
  -rfiledatenewer <file> <rtime>
  -rfiledateolder <file> <rtime>
    where <rtime> is of the form nn['d'|'h'|'m'].

 Examples:

   -fileexists %windir%/notepad.exe
   -regexists HKEY_LOCAL_MACHINE "Software/Microsoft/Internet Explorer" Build
   -regprint HKLM "Software/Microsoft/Internet Explorer" Build
   -regdatenewer 5 "Updated: %Y-%m-%d" HKEY_LOCAL_MACHINE "Software/AV" Updated
   -process mstask.exe
   -afiledateis c:/windows/notepad.exe 20040401
   -afiledatenewer c:/windows/notepad.exe 200404012359
   -afiledateolder %windir%/notepad.exe 20040401235959
   -rfiledatenewer c:/windows/notepad.exe 10d
   -rfiledateolder #REG[HKLM,Software/ACME Software,SomeValue] 10h
``` 

## Return values
Return values are simple text output, mostly with `yes`|`no`where applicable. 
### Examples
Check for a registry value exist:
```
./devicecheck.exe -regexists HKEY_LOCAL_MACHINE "Software/Microsoft/Internet Explorer" Build
yes
``` 

Test if RDP services is running:
```
$ ./devicecheck.exe -issvcrunning TermService
yes
```





