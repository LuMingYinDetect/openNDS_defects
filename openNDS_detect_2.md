Affected Version:
openNDS 10.2.0 99b95176cc26e49a4c092381fe1d04a3e2a1e27d

Vulnerability Description:
There is a memory leak defect at line 838 of the file /openNDS/src/http_microhttpd.c, which could potentially be exploited leading to program crashes and denial of service attacks.

openNDS WebServer download address:
https://github.com/openNDS/openNDS.git

Vulnerability details:

1.At line 730 of the file /openNDS/src/http_microhttpd.c, a variable named "query" is defined. This variable is allocated a dynamic memory area through the function safe_calloc at line 825. When the conditional statement at line 827 evaluates to False, it confirms that the memory allocation for the "query" variable was successful. However, when the conditional statement at line 835 returns True, the program returns at line 838. Throughout this process, the program only releases the memory area pointed to by "fasurl" using the free function at line 837, but fails to release the memory area pointed to by "query". This results in a memory leak defect, as illustrated in the following diagram:

![image](https://github.com/LuMingYinDetect/openNDS_defects/blob/main/openNDS_5.png)
