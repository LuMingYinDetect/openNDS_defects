Affected Version:
openNDS 10.2.0 c392cb41a4c470fd3be0e86c0de088c60262daf6

Vulnerability Description:
This vulnerability is a UAF (Use-After-Free) vulnerability discovered in the file /openNDS/src/auth.c. It could be maliciously exploited, leading to a denial-of-service attack.

openNDS WebServer download address:
https://github.com/openNDS/openNDS.git

Vulnerability details:

1.The function client_list_delete is called at line 222 in the file /openNDS/src/auth.c, passing a pointer named client, as shown below:

![image](https://github.com/LuMingYinDetect/openNDS_defects/blob/main/openNDS_1.png)

2.The client_list_delete function is located in /openNDS/src/client_list.c. When the if condition on line 467 of the client_list_delete function evaluates to true, the pointer client is passed to the _client_list_free_node function on line 471, as shown below:

![image](https://github.com/LuMingYinDetect/openNDS_defects/blob/main/openNDS_2.png)

3.The _client_list_free_node function is located in the /openNDS/src/client_list.c file. At line 448 of this function, the memory area pointed to by the pointer named client is freed, as shown below:

![image](https://github.com/LuMingYinDetect/openNDS_defects/blob/main/openNDS_3.png)

4.After the pointer named client is freed, the program accesses client->fw_connection_state at line 223 in the file /openNDS/src/auth.c, resulting in a null pointer dereference vulnerability, as shown below:

![image](https://github.com/LuMingYinDetect/openNDS_defects/blob/main/openNDS_4.png)
