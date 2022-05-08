Year of the Rabbit Walkthrough

Md Tajdar Alam Ansari

![](https://lh5.googleusercontent.com/RoS-h3FHKr1cGWJWkM0LvudAqVK8SRv_o8KizGc8d6nH3GpfYrD7CBChPlygpQJw2ufCmEKhgTQ3HEIRlHkjWJCxV7ueMhJjGblHoD8RDXPf4kYhrQrLpjO0fxVCqka_w_d29jCb4nohpd4w9A "horizontal line")
I really enjoyed this box while solving it and I thought I could prepare a write-up for it. By the way, this is my very first write-up on THM, so I hope you will enjoy it. 

  

-   As usual, let’s start with our initial nmap scan:
    

  
![](https://lh3.googleusercontent.com/UJG9Qt1b8pG6FSx7SxGCfVlkbz3bnZhLoq-Sb4STKN-iXGpN729ImGd0HoebN72Zn3eA5pjIGvkzQj1wy-ZlUZ_YlS-aL_CPouqpASO65Um3Y3SVl7HlMEUa-cj9fpmQjxSG_zKn1ALORrrlRw)  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

-   Hmm, seems like we got something useful for ourselves. Before going further and performing a detailed nmap scan, (such as using -p- parameter to scan all ports on the machine) let’s start enumeration. 
    

  

-   We didn’t get any message saying that anonymous ftp login is allowed but I wanted to check whether I can login to ftp service as anonymous but that didn’t work. Also, I couldn’t find any vulnerability for the service version for the ftp service on neither on searchsploit nor any other place:
    

  
![](https://lh5.googleusercontent.com/r95Z2KJu4bFYn8yUCnO3tS9Vu12XdVIKWaB4QiygTB8Rh-kGis14apfptdmPMh7KDyvi3a2E6jsV1HIV1gcqHeRe7_lW6mHdT7GDQXe5g3yYGZ2TZToOuvAmLLYKVZz2cQ3L8uN_s81MWNmhKw)

-   Also, SSH port is not vulnerable. So, let’s go to the HTTP port for enumeration:
    

  
![](https://lh3.googleusercontent.com/-pTkBsfxX0InQsQfS3XEvsCo1IxilmwOoPPdsP39NAitirJlXI_lHd4rV2K8ggewtG8RlhK93c_EQc9ckzPkdTtrzk-JIfzE6eB-2X3T41aRG8caN6m8MJlPIaJ8vFiCYirNjymgHTlr5mLr3w)

-   When we go to port 80, we are being welcomed by the default page of Apache Web Service. Let’s try to find hidden directories with gobuster:
    

  

-   Seems like we found something interesting: “/assets”, let’s go deeper:![](https://lh4.googleusercontent.com/wRPJ7KlrHbhIYa_CeUoG_7I-gNFajX-ciKUh4zGD2wl_AvJINDmIwFczkOfy7R1xYmuHMqCqIOgRgqhs1gkn2YyzGa1OjxUISmcAYX5YdTWLuyfT60egtGlsQl9jjtLgHC2wZIrx_ZMcu1xZwA)
    

  
![](https://lh5.googleusercontent.com/T_-i6JA9kkPw_ac5XlRBwpuJ_jJx4YZavC44HsvY_FE2nHjNm3Ls4aMU4SIxdKS9NUYP91MXvgIRNrmDGdFm3VgjX8Lrik0ArjPmkTb2GjtOOzwBKFQkuFM0QyGO4PZ90cVFwfh3BAq3A0wUvQ)  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

-   When we go to /assets , we see there are two files: First one is Rick Astley’s cool song named Never Gonna Give Up, which is useless in this case even though it’s a really good song. Next, try to inspect style.css:
    

  
  
  
![](https://lh3.googleusercontent.com/S11OWZSTHvQRZv2qf0Rf2uef6IC4BsPfHhmhGrVEMyr3sZQ--HYiztanGZKLzjjgNiDVgkM5IG2lNZABDSXupQOkf7gUnAQhmzQcHL7HlAZTgnJVvYm0d4yk70NGIZrDsemTk8FdLOeu8S9FLA)  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

-   At last, something useful. Let’s go to this directory:![](https://lh4.googleusercontent.com/nbFHVUoycInUoOUNt8fW5srSvool_ETin1FEiJvacPjqNp7XFFNTezVZGsbdQInGf7YMGaSxb1dXCYzz6Ik1Xk_IlfH3YUXI3hmjp-b8dhtqgF9QpFY_WuBc2vTSTYbRaTOqJvyTP3blWEykNw)
    
-   Let me be honest with you; the exact moment I saw this I thought there was something going on in the back-end and I needed to intercept this traffic. So, go ahead and fire up your Burp Suite!
    

  
![](https://lh5.googleusercontent.com/2BcgVn00at2blxv87jOwlVe3tt2qLoPzfmxy63Sbvp-kW1osf9KOGOXw1dJVC4VxCvDKK5wOPpVYYtRL8PZxmc42Flv5k9Dxg1ArRpHrQxgkv3a2hMk5EPatuVDHJ24vrbSeIOXwg1aHBjOwzg)  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

-   Seems like my scepticism was right, we found another hidden directory. Let’s go to that directory:![](https://lh4.googleusercontent.com/T763ONOOFF7sZKT8QCt7fOUCAr9zMOGNDraJKxluiZFe-0jqA3Vr_tRUVzh3L5U-br6y7jz9-C_cvAxqD2ASwaelyKflFQMNe10BvJYrb3wvnBL2Go0m5rpLOEl7HFJYYgqQxS-kkCjkVkT8uA)
    

  
  
  
  
  
  
  
  
  
  
  
  

-   Oh, cool! Candy! Let’s see the inside of it:
    

  
![](https://lh3.googleusercontent.com/-Ay74UvtSRIJk-83u6s6rw7zPK6sZgYiNsGK2NLDdDw_UzY2vPZ0D4cdPzu4ldOKgj_VgJGx-MIsvJ8bS8B1UTtK5kssPIHjmNSYvpyixSsfDuYtWB2WXJNNY9IRCIEFnbjuxpf2bD4BV1AzSg)

-   This photo reminded me of the legendary Turkish Actress Gulsen Bubikoglu (maybe it’s her drawing, I honestly don’t know that much). At this point, I thought there was something hidden inside this picture, because we don’t have anything else to go for it. Let’s download this picture. Friendly Reminder: In order to download something while protecting it’s content, using “wget” instead of a regular “Right-Click + Save” is more convenient. ![](https://lh4.googleusercontent.com/XyRczKEO7b35LPafC3BHVyQNgK0faPbFSvhfyJhEkLq4ct4qDfkX2-TkN5n4Y66Xa3Iw0qymZGQ-yFLXxlJ8rn2nhtQUeK5xka-FpwFcOXhNqV6sO0IxpSlVw9JAOpGhE1t3OyXonv3i4mZqWw)
    
-   First things first, let’s exif this thing:
    

  
![](https://lh4.googleusercontent.com/sk7ZE9DJ4Ar-mw9KzCwxh_cGijD6QAEnOwgYzChweYfhPHtC2WOrF7BDhQKGeDwfjIiRWNJYq679QWGQkWiQuoGcunOIiAW7nC56xzRwZHRw1GVujl1A4H5w2j28sGMldoiIS6MYH1BIyTrh-w)

-   Hmm, we didn’t get something that would make us satisfied. Anyways, we still got one more option, strings ! Let’s execute strings on this:
    

  
![](https://lh5.googleusercontent.com/Y4qnLlRUziPPkyAeUTsK7-yeBAwaxuZxJflhTquYCuNRO3o3HJm6ddoYfA3g0KZ7gXr4SRZI1FxTs_enE7nOGTJorox6Wqg3jU-sD9YVLYZ0sk1av-yrdye3DGF-VUjzGmg0jWvgAsyaflufew)  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

-   JACKPOT! We get the FTP username and password-ish. What we can do here is that we can get all these possible password strings into a text file and….. HAIL HYDRA!
    

  
![](https://lh3.googleusercontent.com/pntvj6p05Y00C1sVya7NwYHlO0DQsXJDJ-lYzmt_Ivs4EtB0Qtue182gmUj-9C3RP8YTVYG43AEgdBF_UC9hwQ9dYG4x32MhemBB6FMQNrHZLSZ229OFZD7ux2Nl3lBo9wGJfYj08QsbdVcKnw)  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

-   Thank you Hydra. Let’s connect to the FTP server and find something special:![](https://lh3.googleusercontent.com/Mjh5Q7IfR6B5KJ-nkid1GHI0ImcD1DVrnGa0nc4dB3vtgrCjHM6h6JjvHwDm80hzZ1gUZ2YjroFyRMiwBB1DckgmZ_CEt-mekt-3loeCTpbdPfc9BvRdp6eVsBLlJM0OIM0EgBwh10MfqluFSw)
    

  
  
  
  
  
  
  
  
  
  
  
  
  

-   We downloaded “Eli’s_Creds.txt”. That might be something, right? Open it immediately!
    

  
![](https://lh5.googleusercontent.com/X0xbnggz_gh44_1Iq7YenBLC-rYu6V3MiPok4GWTwCEgUH2hpLKhOnUMtyte2GNCIOFp3rFzePETAM117k7qQJY_X8UXpWCJinb-Ou1Z5Sm7fU0TB1-QhIQ3oMsvK1CVTWrHGZtXBPem5Td_6A)  
  
  
  
  
  
  
  
  
  
  
  
  

-   Ah, shoot. Here we go again. I guess this one is a real rabbit hole. Anyways, after a research that cost me 1 hour, I found that these strings are representing the programming language named BrainFuck, don’t blame me, it’s the name. Let’s try to decrypt it:
    

  
![](https://lh5.googleusercontent.com/pmkKZ-ucFRRiDlCrNSt7G7PSvnz-fAafmqOW0a6-a1_L0ENWoNLEbRqwGFJ44CDM9RkDz_ZN0twfM5o6PiMxKbUnTQUnj2hMhyigqr-hf-xzUfGgl3kDvwr_ugJTo6wG_PZP7Ns3ITHoMcBreg)  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

-   Dude, finally! Don’t waste any more time and open an SSH connection with eli immediately:
    

  
![](https://lh4.googleusercontent.com/plhhdQcI40-PGAM-WfehYRaL3DC5Ha767AageTTL92I6CBHxV4STA1PtSlm5j5Rjblal5FA4OTyYBKxyJ4R4oNnuE-sHw7r6TNj8XquwVtTWXLjWx_reu7Ar3nxjhuEd8_sQltXWwydcOObVlg)

-   We are in! Let’s look for user.txt, shall we?
    

  
![](https://lh6.googleusercontent.com/Mpb90gG9UVAyO73JRCZJCPKDjC7yrU_JRfuESh0Pb4ckxRvumWKSlHv4UlE91frQvrzc0HTt6h5mb7mBnyNzVjjUYZdI3JnYDJpsGQO1ZMGjAQ6rBv0ndQMwaMftVJMpejZkZXe7XtT7_krZ8g)  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

-   Well, user.txt is not in here, nor in some place that eli is privileged to access on. After a little bit more enumeration, I see that user.txt is owned by a user named gwendoline:
    

  
![](https://lh6.googleusercontent.com/DQNnkwGW-Zhg2oNdiQWzTOF-lht7tP6RSZ430WFgQxau335ju9kOWYILiA2mJh6sAlg4hq_7z6X2UfWc8NbmrcPfBUC5yxGO2mqmHmXwpVUzuMG6TKBZYGps3DIj93ePLqr913IEmO_7OpOfcQ)  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

-   Note that when we first connected to SSH, there was a message which might have a meaning for us to torch our way:
    

  
![](https://lh6.googleusercontent.com/UZ_G0hLdN2ZNsAW29WEO08MWLJ0ZnQqBInNQodzMxUHZEfmQrtl0anv57HtVsXhuI5sAu778laHwy--eTkBnhvYjAKqRC8Y-Us9oQ58APrJAKxwuWElEUD_XU-CXS-FYnIdwNUpP1USpHQ6kBw)

-   Dude, there is a message from root to gwendoline! Let’s find this thing:
    

  
![](https://lh6.googleusercontent.com/vjFVXBCM7-huYq8HN68LKBc0vG50vWMNlGG7vKHNXn2G-PEK6KqRjz096BT4DdKSTq02b0hv62OcD9Nm5yzLpgLuKKNrmIGa0UW12JfFSlIWIQtK903c2WDV2cM9BBex243HyXQT25lES7E2Tw)

-   I guess that’s gwendoline’s password. Try it:
    

  
![](https://lh3.googleusercontent.com/x9XE78mI7lc7xbkoPiivDwfcnUah39ba52IOTWG5BVAQEWvnCyVbk--Rh2oxBsPazGlXxcwc8WyT5pTYL_9iSAwh0P7Lj79uf9UcyzRjP5IV4JvZ7Goju0B8v0wzIpMVxbd3Bb-ApbC9FwS9Tg)  
  
  
  
  
  
  
  
  
  
  
  
  

-   Yassss! We got the user! From here, let’s try to escalate our privileges. Firstly, I prefer to check SUIDs to see whether there is a misconfigured SUID bit which can be exploited: (find / -user root -perm -4000 -exec ls -ldb {} \;)
    

  
  
![](https://lh4.googleusercontent.com/g3VZwKmqjwkNtls1AcoIh1wC_92GDMCeJJPSZt44O5Qx74S5OoMIpHDW21pCBpDdPAjrv82tkXzQf7apZoeWBLbEbutqA-s6QGzpIFArPylhVJPz7Dohb-9JB8BR_8Lab0_68Pailvkl-KdYvg)  
  

-   I tried to find a way to exploit the SUID bits that we have access on but nothing worked. Let’s go for “sudo -l”:
    

  
![](https://lh6.googleusercontent.com/LIT1cGsmRKm-gjiIiwLHcI-B8fgzmIcL1TMHSbASilM6SsZlJiH6tkbTqbJzl9HQb0zWiuN1nAowdxJHY2nWYQzj2pECtVf1YkJD7XEtaBCM5FvqF-ZIx25gyNnkK99kTQTPM5FUUNFSfcI8sA)

-   For those who might don’t know what “sudo -l” is; “sudo -l” shows us the sudo permissions of the current user that we are logged on at the moment. From above, we can see that user gwendoline can edit the file /home/gwendoline/user.txt with sudo privileges using /usr/bin/vi. Hmm, maybe there is something useful for this one on GTFOBins, let’s check it:
    
-   Bingo! Let’s try it:![](https://lh4.googleusercontent.com/ajgTkHVmUY-QXj60e3nHl4NoBqkanCOHC5KoKDv5Aumg8eTqS75df7GDSLZlGR3aMy00pDZr8qbA95Etmmt48RcRBnsEqIGNNCyj-WH5MQ8VuOyvzYCyYzEf-okiEOfrL_o7nTfLZqfK2ceNqw)
    

  
![](https://lh4.googleusercontent.com/G1I_jJNgVtt_F7ixhrolNW_LjM9X3z53mZkVE1sIIj2OuCwlBkoqxD4zpHmhIwkrecxPg-yO8A3AiZKWrRa5p00V1UwsdJPdS4vQeSqiwJRvguJ6ugGkPYqeXhbK4cueciQuayDlTDGiPNl2tQ)

-   :///////////////////////////////// At this point, I really got stuck and went to search more commands to exploit this sudo command. At the end, when it was 5 a.m. and when my brain was about to melt, I found a vulnerability that can help me (thanks to Ekko <3), this vulnerability is CVE-2019-14287:
    

  
![](https://lh3.googleusercontent.com/qUO2fxPOcDi1dAQIbh5WX83DPbgaHbBeyvfkgAMFEMuD5bwwXjAJ1XuhtBFy3Ne2EFt6KqpeaRgBb-J9qWXEy35ZboMuP2Upwdnx4GakpR-2Y8kabMOLDnEXM6Be-euJWoj2z-b46U9bhfh_MQ)  
  

-   When we go down, we can see something like:![](https://lh4.googleusercontent.com/GQX2ogboj-rEMO2rcAiT6fsRLEBkx8JABHkik2D9SdJG01FHMV6MJoIuR615sHdetWHC1t2ejnTgT6txB86iUDGiPmrZoNcQ8F6wVsiSL9Sam9P2GBISyYDqP474DypAofKERsXNZi3PozGjsQ)
    

  
  
  
  
  
  
  

-   Yes, this is the command that will help us:
    

  
![](https://lh4.googleusercontent.com/TJUsG6vyWbjydESFwNqi3uH_aUmaOea2oAELjbkfA-LHN9iSEhAN4XuyDmtvoI9XgQHMic9GtaRmG5cvBOR8w_z0reR1eBvalGOZaD5rNTrufXHgzPwWK8Xrlyf7DSXuK-4blqGQkfG_17k1dQ)

-   When we enter the command above, a Vim editor will be opened, then we need to go to the command line by typing “:” and “!/bin/sh”, this will give us the shell:
    

  
![](https://lh3.googleusercontent.com/Eh4FEfq97m5RbmFzKLayuJfMU4dc_7xEYhhLta0QUyiDOGhcTwgBX65B4Wbgxl4cc30223yn3GDHwK3u7BkGXrqr44X7_yel0DcTPZ3U5DCYTXX_5lv-jHqA8Ad2bbdVT_QG13rc_1cSxv8juA)  
  
  
  
  
  
  
![](https://lh6.googleusercontent.com/3o_x97671BU2wp2RnmJ06-NqMvnf7E5KKWubHcSzLjnQtBp8Fvr2ohDNBLCgG4vdquXjL7yT5x5Xwl6AWuQIMB_i73wsqyrKQzP3cm9MQ6eib7Rjh-PR5U7Ow62kgy0CHyaHDibClxvqXnrC0w)  
  
  
  
  

-   That’s it! Go and capture the flag!
    

  
![](https://lh5.googleusercontent.com/bM26gxrBSxnYL_wkt8iX9-1XopevMbW0YNPhb3TmJcQroNbspQyK5Ir-r96tBm6gQRZfcALkGkYPKRVH9lYSQa4xnLw76NvEjV27zlHVpK9IQEbThR4ZwrbnUI8RNdNafdTV0_Yy8TTdThXEBg)  
  
  
  

That was all that I wanted to share you with.