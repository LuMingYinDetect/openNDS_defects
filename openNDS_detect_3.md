Affected Version:
openNDS 10.2.0 99b95176cc26e49a4c092381fe1d04a3e2a1e27d

Vulnerability Description:
There is a memory leak defect at line 998 of the file /openNDS/src/http_microhttpd.c, which could potentially be exploited leading to program crashes and denial of service attacks.

openNDS WebServer download address:
https://github.com/openNDS/openNDS.git

Vulnerability details:

1.At line 971 of the file /openNDS/src/http_microhttpd.c, a pointer variable named "enc_user_agent" is defined. This pointer variable is allocated a dynamic memory area through the function safe_calloc at line 992. When the conditional statement at line 997 returns True, the program returns at line 998. Throughout this process, the variable "enc_user_agent" is neither used nor freed, resulting in a memory leak defect, as illustrated in the following diagram:

![image](https://github.com/LuMingYinDetect/openNDS_defects/blob/main/openNDS_6.png)
