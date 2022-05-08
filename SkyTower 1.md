SkyTower: 1

Report by: Md Tajdar Alam Ansari

  
  

![](https://lh5.googleusercontent.com/cvAHrLUd_njPYcxFCRE2LL2IS9LvXh5XyMt0Y2d5zH9JBZlSVdecfUkt2sDkaPdGJGLnpJs4FxGISQOfB7OZkAedMBJnIO_83rOQr3UyU8pqNoG9xrQxm_Gkl5H93kGSrJnJdEevl1U_KU8qpQ "horizontal line")

  
  

# ![](https://lh6.googleusercontent.com/7SizPLCkj6siOjA1DOzyTFDBkwLi4MA-LINBvqYV2UTGVkDUW-lDBtWjz6NJE3TkiAoRrA2wKgN-nOuZSHxA-ViXMPnnvLkkQCGqiCDGudh51euZuxU7GnyXS5y-f79aGUndVm-t8QIn8YvLFw)

  
  
  
  
  

# INDEX

  

1.  Reconnaissance…………………………………    3   
    
2.  Lab Setup…………………………………………    4   
    
3.  Scanning………………………………………….    5   
    
4.  Vulnerability Analysis……………………………    6   
    
5.  Exploitation……………………………………….    7   
    
6.  Conclusion………………………………………..    15   
    

  
  
  
  
  
  
  
  
  
  

# Introduction

This CTF was designed by Telspace Systems for the CTF at the ITWeb Security Summit and BSidesCPT (Cape Town). The aim is to test intermediate to advanced security enthusiasts in their ability to attack a system using a multi-faceted approach and obtain the "flag".

You will require skills across different facets of system and application vulnerabilities, as well as an understanding of various services and how to attack them. Most of all, your logical thinking and methodical approach to penetration testing will come into play to allow you to successfully attack this system. Try different variations and approaches. You will most likely find that automated tools will not assist you.

Download info: 

-   SkyTower.zip (Size: 290 MB)
    
-   Download (Mirror): [https://download.vulnhub.com/skytower/SkyTower.zip](https://download.vulnhub.com/skytower/SkyTower.zip)
    
-   Download (Torrent): [https://download.vulnhub.com/skytower/SkyTower.zip.torrent](https://download.vulnhub.com/skytower/SkyTower.zip.torrent)
    

  
  
  
  
  
  
  
  
  
  
  
  
  
  

LAB SETUP

  

The machine is deployed on VirtualBox since in the website itself it is said to use VirtualBox rather than using VMware. It is done by just clicking the import button and selecting the SkyTower.vbox file

  

![](https://lh3.googleusercontent.com/TC4rgaXALIumZMFTlVm1pbg7_xnwq0JXo-EXkNOahMATlten3eLvOQ5g04L-Ahu0oLIT0fQT_S4JN13a6ywk2htgU3R_XE5itL7BsED3Ju6227WMBnLYpLHwHgAuV3zW63HPfap_80WAT9VFnQ)

  

As we can see in the image above, the VM is up and running. Please make sure to configure its settings if the VM seems to be not working properly.

  
  
  
  
  
  
  
  
  
  
  

Scanning:

  

-   Arp Scan
    

  

The next task followed by recon is scanning and enumeration.

Using the “arp” scan we will find out the IP of the VM. Use arp-scan -l to list the IP addresses of the devices connected to your Wi-Fi Access Point.

  

![](https://lh4.googleusercontent.com/Ez37v40lnr9kBYuayesP9rRFxUOkk_3UK99mnZ-ltXbxB3R_Mwea9jcmJPbH28C8BY5djvSLF15v-2usI-_NX5yruNw9i1vbWZP1ZSPBnzitzfbLpKktdt7DVmGuGNWE_Qfi2OegcNKoLFezCA)

  

Here we get the network IP of the VM.

  

-   Nmap Scan
    

  

Using nmap we need to find the list of services and the ports they are running on.

For that we need to put in the command nmap -sC -sV -Pn [IP of the machine]

  

![](https://lh5.googleusercontent.com/-N9U-WImvDK7BATBTOLLO4pVEGhDOdjBSQyt64yBLGhV6NzkKUs1pN8f2_QPKbdXNGjXcgdKfOPiFSvYEUmdZL9g3WQxm8NTaOC-yFvdH29e11_A9xPox-U8KW4CmM-vtBeAAlPRI50aV9_daw)

Vulnerability Analysis:

  

We can see that the web port 80 is up and running. So we head on there and see what’s on the web page.

![](https://lh6.googleusercontent.com/IOkh9MQ2u4rSrOkx8u8TFYKqJ8guDwvSxqTk91_EVSqP75w9maF3IMUCd5zlJwZx8Cl5Bv3q9TiUksv6rBz164Ri_sPcgF5ONq_-gBx7CoJ5rO7Ic_HRmcRgRHRnMF4lUnJi62CaQksh0vQoXw)

  
  
  
  
  
  
  
  
  
  
  

Exploitation:

  

After landing on a login page the first thing that comes into my mind is SQL injection via query so I tried exploiting the website using Burpsuite

  

![](https://lh4.googleusercontent.com/ORo75HjEFCVQjZkgCFMuWjUydXlTA1oj-D2GcXkNpFv-mCJqxk99QMuHHSJGGMsFJkIfQurwva8YbLSBblKibi39qg1Xfw437hC7HCdJb9f0hS91xAVRaONd8CnP9cmBzKIar0_z_WZ3vBE-9Q)

In the login page I intercepted I used admin for the email and passphrase as the password

Sending the POST request to intruder I selected a wordlist of SQLi login bypass queries and got some wonderful output.

![](https://lh3.googleusercontent.com/ax6f_DRqgGsgwh5DYET6n2Q1VdYL4Pi2lx7WDHP4uiDzlV8dDTp_gYkIuZLqhejGQ4I2Oas8RWnQz_akCNJJPCl11IgzZZCon5blRVrF2O4tNd3xyCEHAXfCMqE-3O5tuQjCyyApUOBY8sYBMQ)

The request length shows us the difference in the length of the query request.

Using ‘-’ as the email and password we login to find the ssh details.

![](https://lh5.googleusercontent.com/HaapCTjtkk76k2iRkvXPmvZgMmL3IBn0_tnXDDJfLvwdZC0WYXA5rJFThcZHAyXt2TeAgtV-xFBv_0fVT-mkhA5bWn8931vvi0iH1IvWYwAmGj7GEk_io7kWwun5L3-rZ06GCA6PfJbHeDc4qQ)

But here is a catch, we can’t login into the ssh shell. Since it times us out everytime we need to think of an alternative. Being an office internal network we will have to use some VPN or tunneling to get the ssh shell. The thing we need to do is install proxychains.

![](https://lh5.googleusercontent.com/J_x1LGUfa0Xuy1fU82kms4cRYfhnF-G5vRQbrwtknDgLKVbJVBjKTcDLzdB4wJbTRzMLzqo5ZCPBDvRgS_mKOX9uLX3903g6St4jcO4G12n1wTNbJ3vnNxRmmn2Uet8xWQ8zxUM3PidPxbE3bg)

  
  

After installing proxychains we need to configure it to the dynamic port forwarding protocol and set the internal IP of the website and the port that runs on the squid service i.e. port: 3128

  

![](https://lh5.googleusercontent.com/A7977O0arXLHq4Lne2ReYjJc9skIZ7fJv5bY3D3DzqKhZtgpdmzZacPudkhdeXtI3bpl_oTJwOOzlRiSB-ev15iUs8RK_lAXFDP888YYj3xxP4SQ5nq6KBWEo_zCTyJK_FnAmF06YsWc5yVHvQ)

![](https://lh4.googleusercontent.com/xH5gtROs_nFUPyTNouOSTloe3hAqmYQSfR3kGF7fV6DLC7CTzVs9cweNII-ONpOT_iZqGV4LQpBvOx137xSi5LWpJrirSxpH7ZoFAP9sga-pd-DxBpunK6X3SbTSr1Nu63csGpgLThxa2LAV5Q)

![](https://lh3.googleusercontent.com/64sB-6ES_dnBkf5ZHbi1LZliNcrCrimRPyhj09_d31-uwT8cMsMW6YWTbJD5T8dNrr9H24pleXZvqO62QHeV0MTfpwwb4kneByPJCI0STH41NevnvhQXXIY1PBS0yxRgaHvuECgiQkEA_jt36w)

  

Just configure the proxychain and run proxychain on the ssh and we will have a /bin/bash shell which is not an interactive shell

  

![](https://lh5.googleusercontent.com/vd0GvegFGh7o6A_s2CMr6xeZ5xrESCvXvCjlRvKCnhhN4zqLu1v6pz4Cd_kBsaXdgDxLHUD35ChlmOX_P7f7c7z3Cu3ddA78RaeKX9fgxUyZY_52nQJG1YCT2T4eNoKsyaPb-853SNT1rzgKFg)

Trying to look into the user files we find a .bashrc file which disallows us to spawn a TTY shell so we try deleting the file with rm command

  

![](https://lh3.googleusercontent.com/vzjJ7q6zsVGN2B9iPVHAtHrX83CiShW1loLKOvxIkQpgHJ1DEzIr6QwL_uNx28iHJglAylGLIuOAbs43Ws76UuvnS3XVvwpVzYCADShCdh5psrFrMzW56R1w1d6UmKaT6cg3nf0YRbtXRdtv0A)

Now we log out and try ssh again

  

![](https://lh6.googleusercontent.com/8e3ytoXIqjqy1Dux5ZXOPuoNw7_3QQxuu1YWb88w4wnMCxiBnTdEw5uryfJEDx9uXYVH8Rzf9ojy5jy3vS09p82e302_SpgO8vNhOIAKpi0nDuqdonmJkZMeaDXr8iKvyKS8hZfn2uXcTx2u9g)

And now we have an interactive shell.

The user John doesn’t have any sudo permissions so we try looking into any other users in /var/www and find sara and williams 

![](https://lh6.googleusercontent.com/2PADceFjT6vjvEQ-cE6LMHKFpYYXIheizRgVS9K4YEnrjgpNyGOw15EQAyCW5zonJJYQjO1uzX26xnULWMAwc412o_OvigGsFTIGEaHZFKb70UMq8YdhngVNVa1-hLdkQ6mtQF9n5XCBEcOFAg)

Both of them have /bin/bash shells respectively.

But we try logging into sara using SQLi and we have another password

![](https://lh6.googleusercontent.com/BkYzQvkH36vLIV7FPTFfCMjvlOGdiP4X2Xvv8m1zlRb0Pwlfyqnc8ZHCSyZJ03IjBNDjJeUD91B3nHr88LQxPYJhbO3RURtudn5-3lgFPxrGANeveDmh_bffpHbbFy6Y48rhq0tppv1v8n2N-A)

Using sara as another ssh login and deleting its .bashrc file we get another interactive shell. But sara has some sudo permissions so we try looking into those using the sudo -l command

![](https://lh3.googleusercontent.com/V-MdW7p3yOAOtipHFhN7ou0fYtkA1rkLdcqzR2xRx_RjOz2-s6LQuXaAGztOlDDyfcFty7ekgk8Et2Zg1uVC7yklySImZz_H5WiWJ92Om5SUK4Em9RtnMDgSTZxDxQkaPa2AnN_rml4CguM2HA)

  

We can see that sara has access to the accounts directory so we try using the ls command and parameter tampering method using ../ ../ ../ command and following the root. After using the ls command we get a flag.txt flag

Using the cat command we get the credentials of the root directory.

![](https://lh4.googleusercontent.com/J7tKmky-m0aJoSub-bxytwx8793YmFxx4S4jC7ME0H1si9tWc5QzKMtdb6Ddhw2j_bYdEZJ1pGcJ-961OVgUzmFtHFFSk9Oaaajj4GcuKD13r0YsiyL18YV7JWifJWMLf7rGslWrzhLB-bKmHw)

  
  

ssh into the root using the credentials given and we get root shell

![](https://lh4.googleusercontent.com/H0fKGKaHfnXfEGC7Xj7ERC8CkfgcHWSLy0EalJE5_9X4XeMGP-aHazY7BtOBu5R629Sv28k4wpj5US0smliTXdFoEkYPP2yEPBEa8z37NgwAttgpuHN0pBwQUui2IUW8RfCbuY2uTwQzwGuDEQ)

And finally we have the root shell.

  

![](https://lh5.googleusercontent.com/zRSp0XVRKpDRKnS7xWqeVnOARzoh1pd3PSfoDWiwSomORZF3O35mkvAhQahPr2O3ReJJ3mxnhaRN6ocsO-30BpZV1WwSzWOeCDHsKquPQhpo5_pMi4Y6ZJ_MWApPdDLAMTXN2AkkV5kwGjHAkw)

  
  
  
  
  
  
  

Conclusion:

This lab consists of different types of exploitation techniques mainly focussing on SQLi and Tunneling. I had no problems or any rabbit holes in solving this VM. This VM was a good privesc box for Tunneling techniques, especially for beginners. 

About Release

-   Name: SkyTower: 1
    
-   Date release: 26 Jun 2014
    
-   Author: [Telspace](https://www.vulnhub.com/author/telspace,90/)
    
-   Series: [SkyTower](https://www.vulnhub.com/series/skytower,47/)
    

The link to this VM is present at the top of this PoC.

  

Thank you! Have a Hacky Day!