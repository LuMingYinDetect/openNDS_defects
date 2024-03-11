Affected Version:
openNDS 10.2.0 99b95176cc26e49a4c092381fe1d04a3e2a1e27d

Vulnerability Description:
There is a memory leak defect at line 885 of the file /openNDS/src/http_microhttpd.c, which could potentially be exploited leading to program crashes and denial of service attacks.

openNDS WebServer download address:
https://github.com/openNDS/openNDS.git

Vulnerability details:

1.At line 729 of the file /openNDS/src/http_microhttpd.c, a variable named "fasurl" is defined. This variable is allocated a dynamic memory area through the function safe_calloc at line 880. When the conditional statement at line 882 returns true, the program returns at line 885. Throughout this process, the memory area pointed to by the variable "fasurl" is neither used nor freed, resulting in a memory leak defect, as illustrated in the following diagram:

![image](https://github.com/LuMingYinDetect/openNDS_defects/blob/main/openNDS_7.png)
