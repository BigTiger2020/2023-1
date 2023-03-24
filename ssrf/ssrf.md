* Exploit Title: There is a cross-site scripting attack in the front desk of OTCMS 

* Vendor Homepage: http://otcms.com/  

* Software Link: http://otcms.com/news/7856.html  

* Version: 6.72   

* Vulnerable： 
1. Audit the /inc/classReqUrl.php file, in the function UseCurl, call the curl_exec function to execute a curl session, only the $url parameter can be controlled, which can cause ssrf vulnerabilities
![image](https://github.com/BigTiger2020/2023-1/blob/main/ssrf/1.png)  
2. Follow up to /admin/info_deal.php
![image](https://github.com/BigTiger2020/2023-1/blob/main/ssrf/2.png)  
3. Follow up the AddOrRev function, the $img parameter is controllable
![image](https://github.com/BigTiger2020/2023-1/blob/main/ssrf/3.png)  
4. $img parameter input method

![image](https://github.com/BigTiger2020/2023-1/blob/main/ssrf/4.png)  
5. Follow up to \inc\classOT.php, the $img parameter is passed in through POST, and there is no filtering measure
![image](https://github.com/BigTiger2020/2023-1/blob/main/ssrf/5.png) 
![image](https://github.com/BigTiger2020/2023-1/blob/main/ssrf/6.png)  
6. Continue to follow up the SaveRemoteFile function
![image](https://github.com/BigTiger2020/2023-1/blob/main/ssrf/7.png)  
7. The second parameter is brought into the GetUrlContent function, followed by the GetUrlContent function
![image](https://github.com/BigTiger2020/2023-1/blob/main/ssrf/8.png)  
8. Similarly, follow up the UseAuto function according to the introduction of controllable parameters, and pass in 3 parameters here: 0, GET, $url
![image](https://github.com/BigTiger2020/2023-1/blob/main/ssrf/9.png)  
* POC:  
POST /admin/info deal.php?mudi=add
isSavelmg=1&img=URL&theme=1&typeStr=1&time=1

![image](https://github.com/BigTiger2020/2023-1/blob/main/ssrf/10.png)     
