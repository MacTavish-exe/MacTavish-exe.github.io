# POC:

  

## Enumeration

  

The vulnerable host is running on port 192.168.20.213

![](https://lh3.googleusercontent.com/6A1yHQnQ8jwF3cNiGGs6IK_xoURTirYAFb5uWgO1GTW2L47u9GweYAdI9Mj-S7NX9lpGeLZRaENLKc0wGq101Q7bcEGkndICGSsf-cwZgWiePPl0ImWOPyD-ul43RjnSUymzMEw8yFCxJb0GBA)

  
  
  

### Nmap  - All ports Scan

![](https://lh5.googleusercontent.com/0kwRv-kBG7NHk-7F-nxUx52Xyx65omdnGj0Lj_KZ-EWcD8TFhkzE-0us1LItU2v7vQOY1yDFlqOY5ocTfDtILeWplGBVVek67FOCIe0tpD03osklpT1uE8-io6Wku2JbTmiaFYtzsN-MUpWoEA)

  
  
  
  
  

### Nmap - Verbose Scan

  

┌──(monk㉿kali)-[~]

└─$ nmap -sC -sV -p21,22,80,9090,13337,22222,60000 192.168.20.213

Starting Nmap 7.91 ( https://nmap.org ) at 2021-10-30 11:23 PDT

Nmap scan report for 192.168.20.213

Host is up (0.0040s latency).

  

PORT      STATE SERVICE    VERSION

21/tcp    open  ftp        vsftpd 3.0.3

| ftp-anon: Anonymous FTP login allowed (FTP code 230)

| -rw-r--r--    1 0        0              42 Aug 22  2017 FLAG.txt

|_drwxr-xr-x    2 0        0               6 Feb 12  2017 pub

| ftp-syst:

|   STAT:

| FTP server status:

|      Connected to ::ffff:192.168.20.190

|      Logged in as ftp

|      TYPE: ASCII

|      No session bandwidth limit

|      Session timeout in seconds is 300

|      Control connection is plain text

|      Data connections will be plain text

|      At session startup, client count was 1

|      vsFTPd 3.0.3 - secure, fast, stable

|_End of status

22/tcp    open  tcpwrapped

|_ssh-hostkey: ERROR: Script execution failed (use -d to debug)

80/tcp    open  http       Apache httpd 2.4.27 ((Fedora))

| http-methods:

|_  Potentially risky methods: TRACE

|_http-server-header: Apache/2.4.27 (Fedora)

|_http-title: Morty's Website

9090/tcp  open  http       Cockpit web service 161 or earlier

|_http-title: Did not follow redirect to https://192.168.20.213:9090/

13337/tcp open  tcpwrapped

22222/tcp open  ssh        OpenSSH 7.5 (protocol 2.0)

| ssh-hostkey:

|   2048 b4:11:56:7f:c0:36:96:7c:d0:99:dd:53:95:22:97:4f (RSA)

|   256 20:67:ed:d9:39:88:f9:ed:0d:af:8c:8e:8a:45:6e:0e (ECDSA)

|_  256 a6:84:fa:0f:df:e0:dc:e2:9a:2d:e7:13:3c:e7:50:a9 (ED25519)

60000/tcp open  tcpwrapped

|_drda-info: ERROR

Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

  

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .

Nmap done: 1 IP address (1 host up) scanned in 40.70 seconds

  
  
  

## 1.1 - FTP Challenge Flag 

  

The nmap scan result shows a FLAG.txt file accessible via anonymous login on the FTP server. We can download this to get our first flag.

  

![](https://lh4.googleusercontent.com/zXgQPsGjZvqouyWNx3YiNQqHVQHVS4bjOXD_AfT0CvYujA0HwXxdQaa0REzJlG7leDh-uGvBBYCa8_o88jU_dCqcuoGSweQM1qbrF0qIYQX03mRuBFHjjfPg2sZ6ILpFBsuhefe0o_v3r7HZWA)

  

FLAG: {Whoa this is unexpected}

## 1.2 - APACHE Server Version

  

![](https://lh6.googleusercontent.com/B_7RsA_aHjS61PCJ3vUkp63FTZs9sc82k_xGMfB5jh0L9QS5QT0GkfLM9JOU_Gix-0etunhzctYllcNmvdhuoIZiK6fuVt9n_Pzqnu51_YtSBoNcVhZmOkCxIuBMxWjVpFF57qRtr5rA3M6d3Q)

  

FLAG: {2.4.27}

  

## 1.3 - Site Password

![](https://lh4.googleusercontent.com/J0QArO1pWproGoOY3DR8l0aeac_Je2qJavHxbK0Go-NW-IzK_R8bnDWKyx6RunyM6utd278ScqFCRey6KBgZH6nbNzQuF5CJZq550nGZB2MFgO1lrAkJSBKYroN6FIFIh1p0XxHEKTRaGoHLEg)

Using directory brute forcing we can find a hidden /passwords/ folder. Inside this folder we have two files FLAG.txt and password.txt

  

![](https://lh5.googleusercontent.com/Eg7FlJbnrio8htfTQtC2-3ywbles0xKjrn-mlID4tOK33socuoqVmJK3M8puk_Z4Kw9WmoRf20vu5fuUGlkVUs68zh5yuy0OdT56fG1tyNP8dFjB7UCnyPS8PVTLMv4fZWLoHWr3Gol_KSkk0A)

  

![](https://lh4.googleusercontent.com/A-vPSrYo1MgqeJZYOAZ-AvBU7lOjzHiPv9rd_whNTppfdC7ZRKL7wW1EO9vpp53EMAkHzBEHuW4rpNE7GqTFUTMzCrLfBCFrOWiLLkVtVnnY0EcMMOQCgecrQW3sbPNdqJfp_nQVPTNUrKr9nA)

  

FLAG: {Yeah d- just don't do it.}

  

## 1.4 - Site Password

![](https://lh6.googleusercontent.com/M57NiFPk5jfblRswXWXmG7pgD-FFEqHDvnFGqfK3FEcm5VT8GSQwXpc_4Ffjj4oEF10U1KeTzwXE7JlSaMpwPhXPY8GhF8IL0BY2-rCNPlhK3FfoUbVuXPDUg1UZhb0-ADg_H7LV8SytzArlgg)

FLAG: {winter}

  

## 1.5 - Netcat Flag

  

![](https://lh4.googleusercontent.com/L1cWDCUD9Idp1eajnUYSEaMq5UAMknSpuMCO7pgf86j0xeDjsU1T2T1qhX_dniWMcW54gXNKxWBE9ku0Nmum9lAZTnrFN59E_9KQnH_CB-jHeBYGQZIzbkjjBIa68PlwmAnwxt9TPPKnn1kFLQ)

FLAG:  {TheyFoundMyBackDoorMorty}

## 1.6 - Service on 9090

![](https://lh6.googleusercontent.com/4gouWMiMwhgZb6ACqs-m--vqyHq6BLb0urEx08VwMLtbRaYfe-5A5hrIRPTDgcUEIDS4QHmIzUSmk5qqIuvh_0J43uIoL9OAPshYRP7bsOtfBtQCTj4CCU8bL2IeWTl1vUf0B8qADT2ba-LQFA)

FLAG: {Cockpit web service}

## 1.7 - Service on 60000

We use netcat to connect on port 60000 and get a flag here on the half baked reverse shell.

![](https://lh4.googleusercontent.com/PIPBowZN0xEtOp532E-KOCed5-HDyA12NoqHkyHUR6LEg6HGX_anM2S8Zw08mNWCXYHQh0SdY6i_ikOLuP9QhqujYfcSEu8XP60vvqYBSh5buN0mEFnmds2Br55YFSj3LYsexX7TsB0Ae0w_RQ)

FLAG: {Flip the pickle Morty!}

  

## 1.8 - Summer Flag on 22222

![](https://lh6.googleusercontent.com/W7RNJXGsp8xkR44N3ibVh6tGvYwVLP5FEQWuWKN5T6hYf7RFoCKaxV-4HLgwil5HL6oLWNb7nkLDKTotSoMINmlpeb6sV21gcXj91TiTrYd1Zw6cn6mYi2rzvMyDbsKiuo8a6W-mzRmw0wnlRg)

FLAG: {Get off the high road Summer!}

  

## 1.9 - Flag from malicious file

We open a python http server on the /home/Morty folder. And we use wget to download both the  files.

  

![](https://lh6.googleusercontent.com/4bDrKCqRxsJgy9Tpx-Y3Z3MnpMmqBiWiQoWfhQS47TriY4GibMdN5nY1qtVaj5x7hA7x_awCnyxhyJ3CU0-YVarV6BrUQgK6bc9YozSfygUUJa5zkXNFIDOXve8QDRkPLPHvp8_u-9U6sKQHQw)

![](https://lh6.googleusercontent.com/0U6Px4AofZ5Q5FHRem6eRdP3TPDG2F7huag7uCNQq1i-xYF6awI_HjtZpy6Wudo5h2goJb92fGtUr7ni5wWzl5jgJleL3zdo-bu7oh_LCKKhgCpMl6l93TJXqp3H_9gDuOBr05V-1w4nFkk6QA)

![](https://lh4.googleusercontent.com/Gsr9U7Ov3fZkVNlnRrWGC8xfFCMqag_44pxWDv0IH7dvs0BWxkb10yQ72magVNV6RB9JBBOxD498dPrvP5QJyZGUqX6aCnIAZbUr9Kn8kN3WJ3V7VwjUOWcXNQifnhXqKLLd_KEJE-5mgcZziQ)

![](https://lh5.googleusercontent.com/Bx_G9l64KYSLly_Ejw9_UU9_dk_J_M6grK4yEv1NUYGwdtE_-V4ceQYpjXy57JbLkTr64drB2n2ltMhepO7Rp53NRV_qT5udRY1GJGoxmd43UpCQGr4vZ9PQ90u4mw5_O_72bWIdKTBdKSfj1g)

  

FLAG: {131333}

## 1.10 - Execute Safe Binary

![](https://lh5.googleusercontent.com/msUbT6BlUKMIMU8JumgFHEScBZCgucY9Ko0Hk6F3eev_fMc0thczaR_V08pXxM8neM1TMxXRDX3kuG4a8dG5jKKt5OcjUPnZ5qyCpO3pKXQEmgKLrXulQ0jHBxbg1plo3bka-wiZUKd64hHIpw)

  

FLAG: {And Awwwaaaaayyyy we Go!}

  

## 1.11 - Escalate to Root

![](https://lh6.googleusercontent.com/ylrQorUkzXW79AdGW-8sKPUA8cqDb6xNrAGh6c2QT7TeaNaShZKfRrMzbIcArxO5I4Dr32wZv8aNWCe_SNhQOK_BKFFsFoHQ7EUB4tt-_OriJRm6zkr0X73IN0L68_Lrt33STz-Holl1sFaqGA)

  

![](https://lh3.googleusercontent.com/hsbk3uVEofbgu_pEi_E1IYbPk_ZiSjwBzHqlphZQs8QoEXS3kgXU6jGPOlfX-FXnJ6Nz6ZBMf-5Z-UBt6ynyc6thxgVoe5SEkWxwvbx7KqPNvmLbV8yWu5u7Rl3qajVyDrgTpSFq7fNChseePw)

  

![](https://lh5.googleusercontent.com/9LvI_dSAwBM145Mz-j_VTaiIOal2TyKpJ9oalvIpQC9TBYo04kGsKB_YQ6m3Hiqp3-Awi5Vgp1K73Ec0VU0fy94Zb6VGzXuDQuG1l7UTbfz2KtEIW_6YeUGVqrQWKCWw1ePXbUle9HljlsdTVA)

  

![](https://lh4.googleusercontent.com/SZ0cXzUaIcdNED_oSHTvFQ6rZK1VfHp1hHAI0pV1vygVOMCkt1IuI5DFrlx11bAdJzXAZPh-Bu3jgK6eeCBuFAx5TESDy--IQ8RMC-ED2glrENFxgcjn-ekO4837NMUU9V8lto9Qsyh5YOFnpQ)

  

FLAG: {Ionic Defibrillator}