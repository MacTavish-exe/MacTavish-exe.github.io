Ice Walkthrough

Md. Tajdar Alam Ansari

![](https://lh6.googleusercontent.com/zyOz3IAl3yL57j1TMXAnzVPxB-vec90aZtxSsLx6J8hNDX9cs1fVfBEt3bXHDBx68gKmo89rre9AInAW3wK0safWgI2-cvyJv852mcjPzlSf0tdflgMEDbiBKDTK8hEqCbkpD8NRklQvJFGMuA "horizontal line")

# ![](https://lh4.googleusercontent.com/a0c_wbx-UJ59TiBr8xOQUld3L3F7_tYOuWhw4D4IblsroT3_iuelQDCAeVQho4ZonSMERhItnAjo4z4ywoeJdXX-bqCsgMBTQfRRmnPZJO__9NpTltjGWTeWLTf4iT_2kdpMWCWHD6vv05av3A)

  

# Introduction

This is my writeup for Ice. The purpose of this writeup is to document the steps I took to complete the [](https://tryhackme.com/room/ice)Ice, a vulnerable Machine. Which is created by [](https://tryhackme.com/p/DarkStar7471)Darkstar in [](https://tryhackme.com)TryHackMe. Ice is a free room anyone can deploy and exploit the machine.

## Steps are followed.

  

Connect to the TryHackMe network! Please note that this machine does not respond to ping (ICMP) and may take a few minutes to boot up.

-----------------------------------------

The virtual machine used in this room (Ice) can be downloaded for offline usage from [https://darkstar7471.com/resources.html](https://darkstar7471.com/resources.html).

  

TASK #1

VPN

Connect to our network using OpenVPN. Here is a mini walkthrough of connecting:

Go to your [access](http://tryhackme.com/access) page and download your configuration file.

![](https://lh6.googleusercontent.com/0TgEAyEGrzADVB5Pu1P5LjE7QgUSSE9EQQSLgYHbhDBnodvagPK8KX2W7MmeVU1b3-XKXogyDX6AsXY3MUeKGAT7iHeSUyuhV1ZlqpHerAxW-W8-K9vNPUyMJAuMieTfdLRSdXB0ks_zSBhrxA)

Connection Task

![](https://lh4.googleusercontent.com/XcTM95v2bKTTIhcb6ojJeh9KtIaDvwm1EnhOnqq4xwbOLPEaPH4f3mBhMTcxYBlg63DP3EDesDR4VQi4AxKuGFCHJhqq3DtbqjaeUNrgGSv40ZgvtditLdcjP2VgyXycjYQZxoo2FqiIkYydmw)

Internal IP

![](https://lh4.googleusercontent.com/B50cMrubnTleUwMSQ-nvVb8Vk_solIt2ZkjBCChk1SxY4ETimNuNb-v6MSJkxVF7f3RdTMvfdczR6CqNq9tyObTuuOODy47F-dxdMHDnH5EOdUnQ4sZJL853P30MmPYvsSVJsS85_aDsy7o6Yw)

Deploy machine

![](https://lh5.googleusercontent.com/UkP4_qc8t-fDo4L2OXX_di-lq5pBn0xwy6b1Kty1xSlVj_zKPOODQ8Ju3fQ3dFi6iPxEhVbgzqiVua7U2ZB1njnWhTFjF937usJ4K4ffgXH3hKhK35P0KWJ1kMfYCVhS8TsEQy4Ry4TVVIvkcg)

  
  
  
  

TASK #2

Scanning

![](https://lh6.googleusercontent.com/5a5LXv6vwJapX2Kiud2dumxqXYSGvW-DbcOrTt5iVLu8HTadk2dlAjm65TpWaYhj9dTxirrNctJKFMRXeuwcjsD9XsUKoWfmq25Xn0Wy29dmc_eaiVWyBVMVrtULPou_Gz-vBlZrCLDsytNZKw)

Once the scan completes, we'll see a number of interesting ports open on this machine. As you might have guessed, the firewall has been disabled (with the service completely shutdown), leaving very little to protect this machine. One of the more interesting ports that is open is Microsoft Remote Desktop (MSRDP). What port is this open on?

![](https://lh6.googleusercontent.com/2ONtH3XClXh-1ql0gZxQznsLTuO8MGSs0rCTa82gDM-0FkAnwZBmjCcwei6ABcL9foidUtS9INNqJNOCfZsEo4sYQ5mZqSbWmKfmajSHn9730T2SR4nfxkjuW7Tw6mybGiG8OOLNbs0zoey61Q)

What service did nmap identify as running on port 8000? (First word of this service)

![](https://lh6.googleusercontent.com/X0lod_PsyYm0VcFytjO03PZTO_IOmq_QJm2aVgUpyiDgoKoambeIDikPQh6x3iHUwMWFLWIog8T9mRARfKv7VYfLYUIitSuFpWkv0iP5Swd_HUEIRuEu2jXLnW2B70ui5eIO-eOD2JiJUi-RWw)

What does Nmap identify as the hostname of the machine? (All caps for the answer)

![](https://lh3.googleusercontent.com/zccwClgLMQIG8H2EXK6CDsHZbnpi90m4tPdzYcf0AUsTR0wRRjHXjJKZ5vTmO1wTP6EPsqdGnnU0GjMK9fbw_NOJGFEqXAfWA72ebXdQV-wZ8UAgZcckVinkMtG5sQocyGvYys6X8euh9bHQog)

TASK #3

Now that we've identified some interesting services running on our target machine, let's do a little bit of research into one of the weirder services identified: Icecast. Icecast, or well at least this version running on our target, is heavily flawed and has a high level vulnerability with a score of 7.5 (7.4 depending on where you view it). What type of vulnerability is it? Use [https://www.cvedetails.com](https://www.cvedetails.com) for this question and the next.

![](https://lh6.googleusercontent.com/SmJuEkVlc5ofgnPMg7TDIWTvR2DX6AVl5A8TmmfdAG7ahgobrAilAXdd42zasrQ422YcawzC3KTE5m52CQpRdpiGImAXgjicz9RIWEqdGHZuNVzqI8eeq8rxxUq8WggiLZe8KPlF26umngzRzg)

What is the CVE number for this vulnerability? This will be in the format: CVE-0000-0000

![](https://lh3.googleusercontent.com/Qw8vx-j_yjmRadJ6gq2CfWPgMUCtlby9Ukv_e3AXOWfylpWcmCb_nbM6kf02cq-HyxGWIoQVXLE0y70GGd-cEbh5niB-fzEEZ0D1XAGbs-52GxkRkOnUbdJIT6oa_SFgNcCXIOnCp5CfU9UFng)

Now that we've found our vulnerability, let's find our exploit. For this section of the room, we'll use the Metasploit module associated with this exploit. Let's go ahead and start Metasploit using the command `msfconsole`

![](https://lh4.googleusercontent.com/2nX8N25iMOMpMeZZ-xVuLwPvXlHV6rdCyYbT24JmpfaSi388yM9mjHGJ9EJeGbZTV4ArqCq0eS1nuE6475qLZFZjp_NP3rncOqg7ZiGlEpJWyEIde-kFoGYShCf3mHrHpljvWMF6BU3ddNoIzA)

After Metasploit has started, let's search for our target exploit using the command 'search icecast'. What is the full path (starting with exploit) for the exploitation module? This module is also referenced in '[RP: Metasploit](https://tryhackme.com/room/rpmetasploit)' which is recommended to be completed prior to this room, although not entirely necessary. 

![](https://lh5.googleusercontent.com/BD-KIpPpLXb1lubMAu_Q0zrumYnLlW9jxNlHZ0VUo1FFdqFf0W6GrrFIH_0STvOyF1r55Vd0K0Ns9HEFHMV5CmPQoChcIROxhSS9YxGtMBGgppIyxl3Udr4NBjsqv8J7hjuaZnyOerBhfNyV0w)

Let's go ahead and select this module for use. Type either the command `use icecast` or `use 0` to select our search result.

![](https://lh5.googleusercontent.com/IlQkhOL2VfYTV9EWOScBo2WnDV_gNsjS0sdQ3D3x2sQ0IUNbQ2RUzbeuuDBHsJDhdTc49dYr9zujntWTnVsW8ncmN0t5Cjrr-hvh-4erTXXnBDlkDA-WHB-h7sNvacuOarpThiSuqzfGzHh-Bw)

Following selecting our module, we now have to check what options we have to set. Run the command `show options`. What is the only required setting which currently is blank?

![](https://lh6.googleusercontent.com/sbVN-pVcjNHtOvOC4XyKgs58BvhvHXokICJaWiEZl0cKqftPhrFsfLkiVNCXxHbJNn9-KiVHlC-d4azOdg_hXgyx2XM33ETgQdolp8X4CPQ8WCPfe6zNPplhI0g6AakA_eRKOfsguc2sP90jQQ)

TASK #4

What's the name of the shell we have now?

![](https://lh3.googleusercontent.com/iUE5MsLlhdrX8sw-lVVhLot81rxAkhxEaoazYzoohYZpxm8_nzaUO99Q9G55uAyygoTamqjAFwPx7Eyo_ym6RU7PPb6rJPcjX8VRCIbI22mrVbpyK1km665FylgpDnDv8Q0ZfNXQj1-GFHdjNw)

  
  

What user was running that Icecast process? What build of Windows is the system? What is the architecture of the process we're running?

![](https://lh5.googleusercontent.com/FHWvYn0PdZOhB9zw82p5yILO9xl_fLkJzkRG_sndPe1dwXAJBhbnbKWq1giLXhLEJHNUQONNKKQE6SExxnmTWwYxMwy-uj_DqGwCYDh0Z4gNZ3KSNQrX5l7uMCp-pYLXsGrVJnXphmcRtEPBJQ)

Running the local exploit suggester will return quite a few results for potential escalation exploits. What is the full path (starting with exploit/) for the first returned exploit?![](https://lh3.googleusercontent.com/wd6F_bk0DMaznSRbTh0PNdbaekQVboUbfw4n-GhAhTi8Pkt4obuEg8xMHxachE4kiDlra1IImirKAlvg9cZ_UKBg78IXe7PH_Bh0Hu_PN6BuChLWzqXbIPC5PD03K5R2EUvBcJHMCCKnd7aTmA)

  
  
  
  
  
  
  
  
  

FOR THE NEXT FEW QUESTIONS THE HINTS ARE PROVIDED SO I WILL BE ADDING THE STEPS DIRECTLY (pretty basic steps).

![](https://lh5.googleusercontent.com/G002LjAQMuFTTgej4XvasfKTsx_N9S4uIdbD0J5LdCV1a8Gi5FITpuRXxGW5nNIMGdS1zjNJWIv6cknb35NNLbNz59UhtAQU-EDMiC8XIjnkNOMjGkv1FpWQFmsyPxg0vK3desQz_pBvm_9Eog)

![](https://lh6.googleusercontent.com/HR4NNVw53K8vr8_eGviBe7hU3uWUv7E3f25LVX-ViWkHETcH8Tz2eJiVNRALhDQj0LFh7xYfo69aoJTK_xDhiTgj6evDfi-xgYrSUiqV9f1NjgKlrT-TYUuqbNkKz4eHD-8QPHtJDQ-QXp5fTw)![](https://lh3.googleusercontent.com/IRMdHhF6jxY1FcPv1PnoEvY8HeXZPYvRTLx5U_PEhGJtLiYl727DNFmgsKx-4MAHNMeNijQnGH_s3yUMvIhH1oQFTcH9oI8Azqt-u5i2qkdcDIVpWIhZhJBCRO6mN3xOX2zdczp0iOkttioxrg)![](https://lh4.googleusercontent.com/iGuud3rTOIGfvdsbizjNYsWVBzaJ9OpWBRYKclW2V7YFGSJz80ApPdbbGKymH5MvgUtvRQo62D2AkfXcoFC7NL_D_8WH3-RE9foe8-Sbs_860Kk0DGriMwyTBqfqedejhWj5uG5gm9E0Vs330w)

We can now verify that we have expanded permissions using the command `getprivs`. What permission listed allows us to take ownership of files?

![](https://lh5.googleusercontent.com/OPy58kk499vP65RAWmiHgGa6yEz2x1NIR-Q8eyuT6fMjhTeBySGXlrFMtI01lS_SuIQvWbioHGL-DqWcOcXjr6kNOW0KKNAli7WOldU8050dHa6U8Tja5HWKh93R6FTTgAA_LOPSO2GrAj6UlQ)

TASK #5

Mentioned within this question is the term 'living in' a process. Often when we take over a running program we ultimately load another shared library into the program (a dll) which includes our malicious code. From this, we can spawn a new thread that hosts our shell.

Migrate to this process now with the command `migrate -N PROCESS_NAME`

Let's check what user we are now with the command `getuid`. What user is listed?

Loading kiwi into our meterpreter session will expand our help menu, take a look at the newly added section of the help menu now via the command `help`. 

  

![](https://lh5.googleusercontent.com/1nJY_-EY3IFF8__BDZTSTKQ7S8mqWQEpNsPVb_ybizRzVyYIYmwDhI7sdctHvBUXfJ7KtS2znZzx8rDywfw7cdfmRxWbG466BBKWoFoSdpGo3eKh5UBdxb-TjtBcwaJIPkPKurztEVG2lNw1VA)

Which command allows up to retrieve all credentials?

![](https://lh3.googleusercontent.com/jlC23CqkTP1TgsIaoZrXc3A8AsZB712EZyWiky2z8YinqrrTKn-Qf9yf3JxuvAJp9aJT9wjSwpxCRRO9IfVkQjvTky3GV9kTpo4BRZe7AccYPFFq4FShiBEnPmUT-t1NrmZsvbW813r_EoboVA)

Run this command now. What is Dark's password? Mimikatz allows us to steal this password out of memory even without the user 'Dark' logged in as there is a scheduled task that runs the Icecast as the user 'Dark'. It also helps that Windows Defender isn't running on the box ;) (Take a look again at the ps list, this box isn't in the best shape with both the firewall and defender disabled)

-----After using command creds_all  you will get the password as Password01! --------

  

TASK #6

For all the rest tasks I will leave a list of commands that I found while solving the box.

![](https://lh5.googleusercontent.com/VnYfM0WCBhtheWx2VAi8EumEKmXw-sfwvVKuHYp9OGdmdpsu0duVRRngwsAYUtGiPlkLZl6S79KEhniE9vkFFmvOoNTmWO0SLjSlMRv0YGeSw2pWjFfJmRZcjORCRKHRoKYPjxJD6AcF4sPewQ)![](https://lh4.googleusercontent.com/Hg64yy0DENKUZp_2QQ2e3EhNtRcBjHpSG-P7lIYlEqDYDeuKr0OCeGldAUspOTRpHJk-iVEhRNXnJtmQGiriBvYO5jiiaZrbOeATQrrrJf2h0B6wAsrFHYdD-gF6UIYCJRKcJDxPY4axtRpfpA)![](https://lh5.googleusercontent.com/74EjVgP9ezkHMhNCT3v-CL_7R-mzy0Z7BvC63GNHdEx0h3QNqTCoTBSRf8RXXqo2aCuFWRh4YUGQBzb7TFrGREmbX9wMjFEVhqJT71HWSCx9pZKru_XDCuKxUm4vhSNhslNCCWgDtuLu3OB87Q)

  

TASK #7

The last task is just an extra candy for all your effort to keep you motivated.