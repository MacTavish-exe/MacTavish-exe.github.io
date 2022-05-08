TryHackMe: Easy Peasy

Report by: Md Tajdar Alam Ansari

![](https://lh6.googleusercontent.com/ly89G19yjL0eMBAq9zMGFpklO2I-udkNWriVvcmRA72K8Xpd7ougrD_JUqVFynpRewV_dGbd2noWHATsvEnZeibhjBweFCWfonNzZebXmn7acbUfAlUMWeD68G2lEIGVeTlhPpjst35KgCNOCg "horizontal line")

# ![](https://lh6.googleusercontent.com/MgXYmKyTCDQhjcVHbyqC5lI2Tpb6qxpq-iF6fRf9197J-m6bkBVHXdT2xuulbuYZbtTzqG8vabcKzn8EqLfivErV0V8LSfgeRBYusm_UOnkFyboBoe1L6yl59Xh32y-tK9DeS14sl8ViNNFZaA)

# Introduction

This is a free lab, and is a good lab to practice using tools such as Nmap and GoBuster on TryHackMe. And  locate multiple hidden directories to get initial access to a vulnerable machine. Then escalate your privileges through a vulnerable cronjob. This lab consists of Network discovery, Directory enumeration and discovery, Steganography, Privilege Escalation, Cron Jobs and getting Reverse Shell.

  

Machine Information

THM link: [https://tryhackme.com/room/easypeasyctf](https://tryhackme.com/room/easypeasyctf)

  

VPN

Connect to our network using OpenVPN. Here is a mini walkthrough of connecting:

Go to your [access](http://tryhackme.com/access) page and download your configuration file.

![](https://lh5.googleusercontent.com/kPtjJrEeNsmJyhQ4hrhPnzzNyNanJgSLNu_PwECgZj5krHFN8rHZrCl5gSQsXyLfht31XS-vrSEVBx51sBA3DgwJiWwpDSaBmC-tDznXFtXKYebnxt-_wBK17lHgUxmTr7V8UxmXQHGF1kp--A)

Connection Task

![](https://lh4.googleusercontent.com/zu8HSp6XuJ06RwawKF20BFsIUM95e8SV2JLFXYjysNofIaeAGmdAx3hCdp0qqaiu1hWAV6WC7Zk9Hz_VPL-OTOhK6pHx6v0i_MQF0xHQTlMPctqnChAWzznM83sqlGFcsxlvDkRgaayZjQSuwQ)

  

Deploy machine

![](https://lh5.googleusercontent.com/ZFqkucMD_cCW8fUMOEaisjseeVgL9bEue_hfbFdn1rSfPVj59SnBrlcxBVU3_CvN728w9yQrcwWQLirzY1EN3ak769H62O7oTKVSlLAV5vD5VlXsqeiBlTLwmAx5M_LGsy5ZXW8ABRpdX8ZieQ)

  

TASK #1 Enumeration through Nmap

*****************************************************************************

TASK #2 Compromising the machine

Download the given task files and save it.

![](https://lh3.googleusercontent.com/AjhBT42IZRVGkKHESKotlZUb34bXspN0nwUbg5Hz8BlUzK0aqdFu2_Y_kbKUH7MMZYl-iaYC2nqKNlwKtpBHJBYdwu68eA90PYc4ZUE4jdyjNGmRmd__m4_HZpgH2BmK3D-oTeGolWM3-wtrvg)

-   Using GoBuster, find flag 1.
    

For this task I used gobuster and I found a sub directory named /hidden

![](https://lh3.googleusercontent.com/YxNG_aNmTxHJFKOnkByX6j_9qEIDlw50EPDqG95ltsX6Cn-Mc5Ld7QLVuaGCcQvjkiBmHLyOC6S0zc8HDtkasW-Pboz0hbvVRUGEYbFF9PjixLo9nyAL7xxmxVFPVnEHFyfx6OfUTxqPvEvRNQ)

On further enumeration we find a second subdirectory /hidden/whatever

(The hint is to use the provided wordlist file.)

![](https://lh6.googleusercontent.com/8oHgo4sXD_AGQiFmL0Q5z-exAU-3StNvqUrssUjg2nEdF1F9zRncVSZ59UTotzGJJPpUVB-WQIXLBJCNQKv9nLdm8a58s9IFwXuQm3zQYaHIgSg-Dsc8ZBBo0wl2P-algaOiX6n8V60m3xfEWQ)

Upon page inspection we find a Base64 encoded text.

![](https://lh4.googleusercontent.com/2lVXxS0wA2ZfuXe9bfluMnDBUFZib5cUBC5vhkZ9brzLbk0Hjd_knenXsTBWw1P8VVwlFO0IRxTmjgxLmnFXlLCUYMXYoqxc9pngnRdrxH2pcg4FTtlIfpV4F0ojYrE1GTWQYM6UFtIp6q2V7w)

Upon decoding through [https://gchq.github.io/CyberChef/](https://gchq.github.io/CyberChef/) we get the first flag

Flag{f1rs7_fl4g}

  

-   Further enumerate the machine, what is flag 2?
    

For the second flag we need to lookup the 65524 port and perform a subdomain enumeration attack.

Upon doing that we find a /robots.txt directory

![](https://lh3.googleusercontent.com/uM1mf1Crdea2-HEh1VjQnOR5G_i_81JCr9yqEX70Ku0rVIURl5ezuejhymGMQ40psT78_jGQWZkvWwGFJ7m0cYLTqxYr16RpLDz88W0IPsHDut7Yh5ML-JP-1sN3uS0x_iTZWQl8kTzYinIymw)

And the User-Agent looks a bit suspicious. Upon MD5 decryption we get the second flag

flag{1m_s3c0nd_fl4g}

  

![](https://lh3.googleusercontent.com/6lDo32odoe-7YDPPlAKlgi3UnVO_WzzO9vtrRq8VkspgQ6hpXr94pSjKxZ3RZLmrVptGw_SBSkzo-UbmeSW0Zx7fJZfAdBwMM0qApFmJBRZjdujOy48fdp9tgHF9WrpnhvDTBtMqcSsPVZ4yIw)

  
  
  
  
  
  
  
  

-   Crack the hash with easypeasy.txt, What is the flag 3?
    

For the third flag we actually need to check the wordlist file and we have the flag over there hint is provided in the hint section (hash)  
![](https://lh6.googleusercontent.com/GpGSuJAhEVwlIxsrUa84LSZC-s2mBOF7-ko3E4Yt45uoPFFxKupvDxDfnZeAFbc77h--oT86WzbdsLDlwCl3EJubwXFmYJUQFw83TE5rR5e7QYkTyBRlMmKO20tB6us_AHQYTC45EA9WiS-_gg)

-   What is the hidden directory?
    

For this flag I did a bit of fuzzing on the port 65524 and after checking the source code we get some suspicious looking code 

![](https://lh3.googleusercontent.com/TqhUDWNbx4NtNVvL78t89HLsxt15sEMOc6yD8Mh7nveSp6BaAbOL3mD_vwQMHq61h9c6h8RjFobCM_m4qql-Goxc3KYj1TDqvdPC7gWlpYzRecIUr0_QYSmkZE05LE_Uo9oJe2oojs5drzzAmA)

It hints out using a Base encryption so I fired up CyberChef  and found it to be a Base62 algorithm ciphertext which outputs to a hidden directory as /n0th1ng3ls3m4tt3r

![](https://lh3.googleusercontent.com/UbBD9B6rzCgxCWfjCVRTEvxRTrItYb-otC_SMgd1C1xeDDnQBL5TscK_iFu26AnchnzXw91uyF2yCeijK7w7qWW0jbllawvpwEiM6N7GCRIRQZXIFZr7cqvPutEItZw-fB5yZ9-85pkTDQb31A)

  
  
  
  
  
  
  
  
  

-   Using the wordlist that provided to you in this task crack the hash what is the password?
    

For this challenge we have a hint 

![](https://lh4.googleusercontent.com/VTEGHVCDwCfH721vrWDGoigm6rGWl2l3U0RfUr1uxAekiVN1VBofAgNEo-wEgrF7RJqz9ES2NTWKDHHC2HRT7H2x9OKJUAKjzBICSC3WknM6533porw_3YxUFwUywgyk_-1nk3Nu4JWk7PFUJg)

For this I compared the two wordlists and deleted matching keywords and after curling the website I found that the hash is 

940d71e8655ac41efb5f8ab850668505b86dd64186a66e57d1483e7f5fe6fd81

After using JohnTheRipper we find out that the hash decodes to mypasswordforthatjob 

  
  
  
  
  
  

-   What is the password to login to the machine via SSH?
    

Opening the directory we get a landing page 

![](https://lh4.googleusercontent.com/1gx4OnjxsbeX0ZOHjL8XLS7531Sd0L7xybqShF_N-pepPjtpaS5e2J3x8M3VKQYWu_9lwPQZSHCEk9Bxsh2X9HkmFsajitoHRgI-whbpwjNrOvoUvPayu3jL-DcOf8a8hP9ZsECUHIyIxswtUQ)

Here we find two images but after decoding the binarycodepixabay.jpg using the given password earlier we get a file named secrettext.txt which upon opening gives us a binary code

![](https://lh4.googleusercontent.com/Z7uSgoHR2xsBvG97Ebqlvf1J1r_uCwgGSktrqbNtdX5rL_UwRN6mi_yXf8u9-E2m3XHU8o2h7SY4Z-omQlW9YeDFh7lFPND80OP4IkNdl-obkmJPw_1zjXRtm9_Z2syjGohsqlZjURddZGqxnQ)

Converting this in cyberchef gives us the password 

Iconvertedmypasswordtobinary

-   What is the user flag?
    

After SSH into the box we get a file named user.txt which gives us the flag to the second last question.

flag{n0wits33msn0rm4l}

-   What is the root flag?
