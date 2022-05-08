RootMe Walkthrough

Md Tajdar Alam Ansari

![](https://lh5.googleusercontent.com/RoS-h3FHKr1cGWJWkM0LvudAqVK8SRv_o8KizGc8d6nH3GpfYrD7CBChPlygpQJw2ufCmEKhgTQ3HEIRlHkjWJCxV7ueMhJjGblHoD8RDXPf4kYhrQrLpjO0fxVCqka_w_d29jCb4nohpd4w9A "horizontal line")

# ![](https://lh6.googleusercontent.com/JaJq9KOx7IvWK22L8fKvlytXo-kz6MPlI9A0SOdxb-rIxiaVfYE2139BDLp8yh69OZZ012zdPE-5unTr_IIseoCslGLam6Pc4nNUpbT2biSjWdNMrKq1BPbhVXlIFRjIRj_hUT-NbFLJNYjnPg)

  

# Introduction

This is my writeup for RootMe. The purpose of this writeup is to document the steps I took to complete the RootMe, a vulnerable Machine. Which is created by TryHackMe. Ice is a free room anyone can deploy and exploit the machine.

## Steps are followed.

Connect to the TryHackMe network! Please note that this machine does not respond to ping (ICMP) and may take a few minutes to boot up.

-----------------------------------------

VPN

Connect to our network using OpenVPN. Here is a mini walkthrough of connecting:

![](https://lh4.googleusercontent.com/RIPZNR4RiNvtaQvT0tq-nw-gA_wiZM1KhJ6svKowTGF0FxYpe60Tol1-ycteQY2un5-yo4noIECzDQLg2epedOCL3RpKuu4wsr33ztBlmOav4nmgEfR1IZWSZYi3AssnVmKRvV1ej5bXrMTfug)

Go to your [access](http://tryhackme.com/access) page and download your configuration file.

  
  
  
  
  

Connection Task

Open your terminal and type in 

sudo openvpn {YOUR VPN NAME}.ovpn

TASK #1

Deploy the machine

![](https://lh3.googleusercontent.com/LbG9cBBwALrht_N4LEEOWT_su5_D9ySeoUTl79qQZ00n9C3nYhY3nGQ-zO6yuPS3uzF8BgdqQLbwgXF22a2ZPZfYXeeh2xsXm6vh6GhMfAPd0uidGvvEOgbnNnQ0f7vLR4O0SoOyBRcrQ_B3pQ)

TASK #2

Reconnaissance

Scan the machine, how many ports are open?

What version of Apache is running?

What service is running on port 22?

For these questions we will use nmap.

![](https://lh5.googleusercontent.com/HC_WUg9ZEKxmEEZKW3Fm7J1qW5IobDb4yV4vH4ifXPhjOPX-6Vto0SkHYwr1naNCyDd7CtuNDfkXAQXaw2eWfsSliJKChAsIjCFOy98VSB651Kbp498fWZp9ZHiIIsMu3aPhaaEeiXgtom0wdg)

Find directories on the web server using the GoBuster tool.

For this use hint provided

gobuster dir -u MACHINE_IP -w WORDLIST_PATH

![](https://lh6.googleusercontent.com/WfWq7lLrZlkeAzgd3IToV5qpYd5DBri95shHRd6Ub2NNL0PkblrMSpIUCWU4fnrXizUKDD3kY2M2JpsoPw7qhLgOCQSHDrcn-z8sfIrQkoN0fGgVPtLsVtSBQXSueAjg2NarczQcU3F73nShlw)

What is the hidden directory?

Trying to search for each directory we see that /panel/ looks a bit suspicious.

TASK #3

Getting a shell

For this task too we have a hint 

Search for "file upload bypass" and "PHP reverse shell".

Be sure to edit the IP and LPORT on the code to your machine IP and an open port to listen using netcat

[https://github.com/pentestmonkey/php-reverse-shell](https://github.com/pentestmonkey/php-reverse-shell)

![](https://lh4.googleusercontent.com/zVNMmCtyzgJhxFqtWEKxP9BD_fJ3c24iDnHmkdoMRDHz2IX2ryPV6ePYBuuDbGU1UQ_ZO6g9ssJ4iCU8iwgRnZG1U-TO467YB6U6BfgIdZVD9MckeFBEEdkvEKkZh90k3LQrnu-Y_P4NKrdBOg)

  

Now we need to upload the payload. We find a directory to upload a reverse shell as a payload.

![](https://lh6.googleusercontent.com/XBWQTAYqK5bQJSr_Gj6-_iczsopvaUHLjQBhX1N6hBmpohdBKqIJ81gjUBlEM_InK-dhx-fLp5BV6MUBkw5ofMgqLqnZFccZolp12Fc2GaJ15Os0-I9ByDhjRNPGiptDTZlirPuvYZN_8RdwbQ)

But there is a catch that we cannot upload .php files so we could just tamper with the extension we can get from pentestmonkey. I used .phtml since it is executable as a .php file so, there should not be any problem in that.

![](https://lh3.googleusercontent.com/8riGIrx0qWMEIDRMb1qcU1QLEpimNhcjbjPYkOdAggs5oHPz6lUyWYqXd06I3Fre27BTruJozTDr-WlwWoH3eDdnHQ7MtKDk6F11_ylUPQdYYGqnWg09tNwUyOZ9F5KtgykXsrVtmyFkGkEtiQ)

After the file has been successfully executed we can just run our exploit.

![](https://lh5.googleusercontent.com/t5w2mIXO3Ft2sxPk8X_RaCyvBzkWV2NKiZr-3h8-mhDpXgLQ90KnlsXnndthucoMhdh4ezvRGHis3ZPidmIdykVJDhsPJtdyJFK92b72kTTLBzvZvk_eVm_QFLXx06BntJAcsgfHF2VWoVdMPg)

Now is the time to gain a reverse shell using netcat listener on your specified port.

Before that use curl to execute the code using the following command

curl 10.10.251.158/uploads/{PAYLOAD NAME}

And then search for user.txt.

![](https://lh4.googleusercontent.com/zPJkc9eWTBRzwnY2YiNkSz2dCS8uAuJVmGn1Kg0ZPohmKTuWqPVTZkuyyMSKQY1xjIVDd1zKuFewyig9mAZg1YAMkNynkjlj8ityNMg_Cqh-ADD2FEmuxMUYnCUNGk2Ej6DEG_K4ndxK5zo-2w)![](https://lh5.googleusercontent.com/j4BBG7aKjEMVlNDlAgQet8TB1NjOHbJihQIBDhs3WH0ZAD0Q5hsTcfMbIhiebn-6sI1Gg4V6FHRKcpwKbk6ltp-1bZrcZbX5SYJRCSGx7YPzdmv-VLV0jzMKANYGEtzfEexTwNY9cRMB-HWr9g)

There you have your flag.

THM{y0u_g0t_a_sh3ll}

  

TASK #4

Privilege escalation

Now that we have a shell, let's escalate our privileges to root.

Search for files with SUID permission, which file is weird?

Use the hint provided

find / -user root -perm /4000

![](https://lh5.googleusercontent.com/2alsIhe4QB6kHQs_EuulOKb65dbmlsZ3owrzLfctUtR-wPe9mYwZqOLgFOauKW1pojf4GLaWeYle53Os8pDL1zHqVNQk2EudatLZ5Iph67kbwWXdZ1vygce-adm0vpe0NE5m8ooXZwwaMgesPg)

  
  

Find a form to escalate your privileges.

Use hint Search for gtfobins

![](https://lh4.googleusercontent.com/FgRowPtzd5qb_WgFs9ZfDOspQB-mrnkCX7aYM0oSiFbbi95gDyevQ2bUjzJTbs0cLghE2jCFKoB1hYCTHuq9eZb_FKVZNDOaDGViv9m_o6_LIgANFIJu_e0z4ycRgPeX05BxnSfni5TpMFCi4g)

Now lets get root privileges.

![](https://lh4.googleusercontent.com/kcqEuD487GJv0RPOjUoaS8JNTeD-69ARMAmLt87AjrX-EUWGreFHxMw4-r1H-kjK1492cPfn2CAZZ9CLcTykKSIcAwOFcKJGan_FQ6c1oqxiPfU-3vCbhE_VMLobyqn-Cbo0JpuhpTLcXj7_4Q)

Type 

ls

cat root.txt

And there you have your flag

THM{pr1v1l3g3_3sc4l4t10n}