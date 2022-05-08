MyExpense Walkthrough

Md. Tajdar Alam Ansari

  
  

---

  
  

          ![](https://lh4.googleusercontent.com/5HGuZ4RA3APkR7zDPz_diBCk0ZE0sRF90woF562D2lPDDtZT5rrJRxIF1A9I_y7Zl2EpBb3WweWngiaB1mgtt2slY5pAyICtk7cDq0vL0Y4xFNNzA6oFIigmCLH0Z1TqvPrZ19RowRW9WwIYBg)

  
  
  
  
  
  
  
  
  
  
  

INDEX

Contents                                Page Number

---

1.  Reconnaissance…………………………………        3
    
2.  Lab Setup…………………………………………        4
    
3.  Scanning………………………………………….        5
    
4.  Vulnerability Analysis……………………………        6
    
5.  Exploitation……………………………………….        11
    
6.  Conclusion………………………………………..        22
    

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

Reconnaissance:

MyExpense is a deliberately vulnerable web application that allows you to train in detecting and exploiting different web vulnerabilities. Unlike a more traditional "challenge" application (which allows you to train on a single specific vulnerability), MyExpense contains a set of vulnerabilities you need to exploit to achieve the whole scenario.

  

You are "Samuel Lamotte" and you have just been fired by your company "Furtura Business Informatique". Unfortunately because of your hasty departure, you did not have time to validate your expense report for your last business trip, which still amounts to 750 € corresponding to a return flight to your last customer.

  

Fearing that your former employer may not want to reimburse you for this expense report, you decide to hack into the internal application called "MyExpense " to manage employee expense reports.

  

So you are in your car, in the company carpark and connected to the internal Wi-Fi (the key has still not been changed after your departure). The application is protected by username/password authentication and you hope that the administrator has not yet modified or deleted your access.

  

Your credentials were: samuel/fzghn4lw

  

Once the challenge is done, the flag will be displayed on the application while being connected with your (samuel) account.

  
  
  

Link to the VM is: [https://www.vulnhub.com/entry/myexpense-1,405/](https://www.vulnhub.com/entry/myexpense-1,405/)

  
  
  
  
  
  
  
  

Lab setup:

  

The machine is deployed on VirtualBox since in the website itself it is said to use VirtualBox rather than using VMware. It is done by just clicking the import button and selecting the MyExpense.ova image.

  

![](https://lh6.googleusercontent.com/DX4QXguouOqvUCKHW9brRuZES6abzzi9zluI7hrW6WmAuAQVSIc9u_Dw7CVT10XrdMjXA1eeG3oaMuH-EKYOqB-elv3RxToiauJQfLB-qwGvcEDdl23LhxUaBhwab0X9eFC4W-R-hCL794kNyQ)

  

As we can see in the image above, the VM is up and running. Please make sure to configure its settings if the VM seems to be not working properly.

  
  
  
  
  
  
  
  
  

Scanning:

  

-   Arp Scan
    

  

The next task followed by recon is scanning and enumeration.

Using the “arp” scan we will find out the IP of the VM. Use arp-scan -l to list the IP addresses of the devices connected to your Wi-Fi Access Point.

  

    ![](https://lh6.googleusercontent.com/ByfMYPyupgAD1A4fypWfRPJLVQ_1mrtQXqjwJcA0rV-AQ0TQbOJJDJzVrcw_SN3R-DGRXIJWYBMfE1upLy6ZrYtcwZc3qK0G0NxQisXwx3NDrBmT8_fH_ESlhnc61iZ8kUuPe4nQQAaLRGXvtg)

  

-   Nmap Scan
    

  

Using nmap we need to find the list of services and the ports they are running on.

For that we need to put in the command nmap -sC -sV -A [IP of the machine]

        ![](https://lh5.googleusercontent.com/2bVzU_Uh3JrwMaMn7tvRJ-QpsAG8Kf8pmB6llN8cRosKEVO28Jk7_55Jhp74WGR0lt8xzT6Gr_EOKxIvaVSHlXGIcV5RgsZKh2YL-yyNPnYosg-u_a0fR3bfS8tv5kWCIOgF6LpEYFlvE1-BUA)

  
  

Vulnerability Analysis:

  

We can see that the web port 80 is up and running. So we head on there and see what’s in the web page.

  

    ![](https://lh4.googleusercontent.com/Tqh2gqm8mBJb72vzOx0LUT4DGHdKfqR2-z4wTL8xICcIiIbfcZMOngXCehSGRPp-R25YmyTVDmRpuFC0DShiCBLjIqLehtxQQ-NN8Div9b2kSBq7rRUkZWAW9XcpIUrkgg5LvRC9bSu_7HyfrQ)

  

We can see that  this website is entitled to some Futura Business Informatique. 

  
  
  
  
  
  
  
  
  
  
  
  
  

Performing a dirb scan and then checking the results gives us these results.

  

    ![](https://lh3.googleusercontent.com/iPzJmT2t8RYIg9TJ6v7fHgfvQagzU4Fvzp4qp9x3DVDVXwsmTb-SbP4xJI0VvfOuRzMZx4BMcfBiF8BeCcWY3uTVllqDaJnHpIMj_y_8zURPxKYw6LlIHA0Y86L1OmQR6hu_KeyV6cVBMBMrSg)

  

Here we have the robots.txt directory which leads us to an admin page. Which shows us a list of user accounts.

  

    ![](https://lh5.googleusercontent.com/V621_M2nJ284P9ZSylbnhUtnZFJZ3LOKPdcYzuVQTyo_ADQaHiZbe3UOmKhfrIvgSr4EdOwuXnHlvdnooZpIAjSTvKw_eYXMd6lvOz7DhmF8mqDU72K_4LGFW1eSv3GgBtV494uxTkAF2iFzYQ)

  

Here we can see that the account of Samuel is inactive. We cannot activate it since it needs admin control. Let us try to create an account using Don’t have an account? button. But it blocks us every time so we need to inspect the element of the page using Ctrl+Shift+I and here we can see that the button param is set to diabled. So we need to enable it.

  

    ![](https://lh3.googleusercontent.com/jIU5l1NVc7rLLCYh5GY-YK1BdC_LmPYVNdROxXlv7k9l1cBs4-RxVUCySPwv2_gIlZ7hYf80UZHSrFNyN2gtfEFeNWyw1uVPBBqOU3z_TXBULSqoKSt-Uy9ZX5Kq-oLhAj4gueeC-LR8-6wLzg)

  

    ![](https://lh3.googleusercontent.com/-Ti7DOhUuw8QyUrlXA2hkpHGE3_5O3D0dlnAOs-QcvZYgrpyyKXSLciK16LIEi4Ys8Jd63BXydk_W0cI7cC00TDDAo9A3bgjwjBuYkXcKHlkTD5TuxdV8ymYxPFZYblwQoP7UHWO5JV-yJ69UQ)

  
  
  
  
  
  
  
  
  
  

After enabling it, we can create our own account to check XSS vulnerability.

  

    ![](https://lh6.googleusercontent.com/wdM_nqSOx4wlyCVYNZLIxE-8H36GzzGjFD5CL0I9LS9rsB2CGjGF2cSdjrCCRXc6gVnYgY_0b_r0TioLmWmWSBOUoG4GGp8CD2X4BvX2XWVV9XMjmY_vIUSGlnEXcrIK5-c9k70I2mtCpOAciA)

  

And we can see that it is XSS vulnerable.

  

    ![](https://lh5.googleusercontent.com/Xi3EqaEhhB3tUddgTd4TGjlOqD6ParjavTzoXinfVgHwZUzk_MfH35fyj7sIMjI5kpzFyejhvrDgewiJygZxok5-NA0jhbVAn68UtA7df7lGruS60gt_ArkbwC1R4hzc6duerrqUNU91qA4AcQ)

  

So, the next thing we try to do is to activate the account of the user Samuel using a method popularly known as “Cookie Stealing”. 

  
  

Exploitation:

  

To steal admin cookie we need to use php poisoning scripts to run into the webpage and return the cookies of the users back to our base machine.

For that to take place we need to first shut down our apache service using the command “ sudo service apache2 stop ” and then write a script in php to steal the cookies.

  

![](https://lh4.googleusercontent.com/6oZqRC5gpQafN3_WkO2QHfWja5SJBJ11HUo_8Nk02eZFk1lJzq5Qg1WucritnJz-Jd2_MRfgcIOPfAXQtv88sDMbBedpUnF8KufZIUGLPw76OEKY31qt7zTkP792D6yR-NvZTCOY6gssiK-91Q)

![](https://lh4.googleusercontent.com/Sl5X7_e9_xmzNZfl4gCgz4PPQxuMSASEdajmdlBSg38vD2cVv90MLRP573UoeWhBeUeBACZkIpw8grtt4aMIsIOYQ28FkjhrlKxMe8MiG9bzihU89YwEssUVtSXzG-IqIEjzmyQobNgwfUsPaw)

For the time being we will use this script to steal cookies and remember to save it as a .php file.

  

Now we need to run php services by the php file we created into /var/www/html/ 

  

We are going to do this by the following command

sudo php -S [Base/Local machine IP: Port number]

In this case for a web page we will be using Port 80

Now we also need to run a payload on the web page. For that we are going to use the payload below.

![](https://lh5.googleusercontent.com/fl5ing1nxouCp44m9omfRB0rYRsmKnOKp9gORcDDkd2sje0hvc4ZWnqEoZB7XXvL4WEKAeB3bN60nOqr78C677cHroXS75rV91EfyiyZjibHSstqUJxW5ODZSGlJ2t-smQTxy9Pei2Q17XRGtA)

  

Now it is time for us to use the script on the webpage itself.

  

![](https://lh3.googleusercontent.com/hIh_WY1fuJpTuxEhONSaPaeDkMMT1vEOQ16UD1jaLHZ_onyECAWws6osz3wWdaj_kLHQzu_gIA7-AfDvUZszovcI3lM5KRuoNuw4WwY2gogLF1BYpAKMvxLAz2-d4q_6ILxbdHdX8gvRmVntCg)

  

Now we head back to our terminal and wait for the cookies to be returned. And voila we have our admin cookie.

  

![](https://lh4.googleusercontent.com/W6-wKWM2zHVwv85AXIR5nOgyEtuxBU_6dfajakFUjo4W5QW1Vd0kgGPf8Oc0O9qqFJ7IVNjrVt-jf8SOb0wuYWTT-AJV8MfH47LutFDzbN5K2G8H_iC5621wA5RZRVqet26IOyTTU1IKfz_J5A)

  
  
  
  

So our next task will be to edit the cookie using the cookie editor addon.

  

![](https://lh5.googleusercontent.com/IVf1q84QlPqUcpUkLs9nRH828qh_XLxY5VaubjGjG_FYwx0mWdRqS-F6nEir3e4CWJSPte8Y0oZ5sXnG4CbsX9jWwETCDwgc9FXqIQSSV7Bauj1mQaWCWuH72chgzFeXPs3ONlIcBRebJCAZRw)

  

And now we have admin privileges.

![](https://lh6.googleusercontent.com/3_srf8iua7zB9NVulm2zWWRXF0-2ik1ihAiGDogb9r_Mc1i4ZQeK7gsEy9PXzlqdIiDhCXck6X7Hm9SyWmHRS6sY49EdXNTf8YgEORyOFuTyWflgcQpgqAlylupYPCvfYEklCYOwxGGLrIQ6Hg)

  

Now we need to activate Samuel’s ID which is 11.

  

![](https://lh4.googleusercontent.com/MN2kuXHdMZlc2hQBEShWnARKFr_DiypE7d8h2BdfX641_U0X-GvDWvlw23jJAnzyRln54ofTkQHpNa6wPAIF2_Y4fwFA17ccK9L8N8-u8QtUru5HAvv-lbWWkHdiIiAwHmMe-Ntm3JUf26m95w)

  

For the time being we will use this payload on the /admin/admin.php directory by creating a new account taking advantage of the XSS vulnerability.

  

![](https://lh3.googleusercontent.com/7Zp-JbY2P6dLjxbIGEd3sgZWESM-SN0Tl53t4Ovg2nw5hOExN3ZumY0b9hbBHXR_YFXivbCwOG28g21lrM126KGZ_jJRBei08yvqrKmcrCwmvs4ktfLMhl4RBcE9a2LOQ7vd31fQSz0Dk55jLw)

We can now see that the id of Samuel has been activated.

  

![](https://lh3.googleusercontent.com/zRvBl8Vps8AroXGowiWLTpqtwQpWyeLfL2bQ0ekutodfxn49wSMWxjQkWW8MA2yjd9t32oMyaIqZf7V8_AgbvMeVZQOKV80ssekUMGcr_iMK0IAiFpLzIpdH4ulI0cRCkUExceKD8x115USKjQ)

The next thing for us to do is to login into Samuel’s account using the credentials given to us.

  

User: slamotte

Pass: fzghn4lw

  

![](https://lh6.googleusercontent.com/ZJ1LLAIo1OBA3HDwE0NA4dkySrL5C8Wazn5ZcKaPQBAzWXw9i9bnhfp8WLyzHubMeS-2Ygl94c7E9pP-6XqqtfDrVkp3CcCz5gQwT4HjPgObTZHHHl37BkPC9MMUNX_DQ2NdHeuMVvrgQrkSPA)

  

Now we need to fix the things that Samuel needs to do. We have to click the tick mark completing his end of the work.

  

![](https://lh3.googleusercontent.com/w5mqMT4MjRGZAaI6-Z2BF75o8naDuinMu_ehwk3uCkt3MRnr3rHRh7C4O_xcBpeoVwPDQrY40oOWz-NN2EZdLnr8DD6PAnDNSm76Fqv-qqhLql54CoF13aKsMYgJ1KDsb_R9-Ge5E72YSQpWyA)

Heading to his personal information section gives us the name of his manager who is going to approve the work of Samuel. Using the cookie stealing method that we used earlier, we need to find out the cookie ID of the person named Manon Riviere.

  

Before that we are going to check if XSS still works on this page so we are going to make use of the comment box for that.

  

![](https://lh6.googleusercontent.com/Q8cYxk0iQzqqjv8dg5fDRORDBBdFu45XL-3Iboc4N1hQfiNoLI2h6bTtABAW1GxOfdHWxOk7-CPjH8hdGdUwHL5QTHyOOjIY22VUQJir7eLOWwCv6l4q4sss2DMJJ3F6O0iBgljk07sG17XX3w)

  

To our surprise it still works.

![](https://lh6.googleusercontent.com/0mIIj385j7B5XmO5n_nIoH8auUlYYP-MIpyRI8c4LniT9o2skRKEcqcoLff-qVIvcaq8QTBYof_htRG1u9tB5YNEA7hpk-m0guGwVgl2ZDsM_Xg9uQCSYL8z2xQ6s49cvfYzTlz17AUmi_bb0A)

  

Now we need to find out the cookie ID of the person named Manon Riviere. To do this we just need to edit the name of the cookie and save it to the exact same location of the previous cookie stealer. Here we are only going to change the name of the .php file to save time and less effort in typing.

  

![](https://lh6.googleusercontent.com/eo2l0lWS4ARjw1oKpL6xtvv2Rkj_EfVW-uDtofV8PKzt5w3_L7Wmqm7ukP6JJJRw0eojQ2AZ9Bl8celi6H8LIIxixMt3OQhZut72wzdxbBHN8uIsKjFvf4WIbFgh74q4hchu2HIL-LroZ-kflA)

  

![](https://lh6.googleusercontent.com/hio3DPkqGLwr9mcBCcxunIhPGYcq8qs8S2WPzBxNk4wSojIPiUeWnDVYBkq8QPGh9Qa-CCLUCsKT6eRPiYjC-dgYZGmHCn6C4QVsqbYS5QsdVnz_KyLqeUAIFkx9VgINKBcKAqZTWjI6zR8GxQ)

  

During this process we must not forget to change our local machine listener to intercept the new cookie ID. Going back to our terminal we can find that all the cookie IDs are intercepted.

  

![](https://lh6.googleusercontent.com/gMk0EOw9A9j1PwGGacNh5FGKFFuyq9RHeeNlxqYMPppTAJHmCO-SQ4UJI8mdD0evPiSN3e-bBv_xA8hLjmIuofteZLqNNFQU49MfN63x9GIBEfqG59Vj8MFY82brMy0R6-ICQigksLMMbd4wzA)

  

Now we got a bunch of cookies. Cycling through each new ID gives us a different user. We need a hit and trial approach for this. Trying first Cookie ID gives a user until we finally find the ID of the manager.

  

![](https://lh6.googleusercontent.com/h36WVs8QJLcdJxC_1wLRSbtkEIf-5kteH-T5nqnkLEXHJTPx4-PC0asRe4E-CUC_UTazg1tM_apTyg0OdFq2Of1wHCOz8gLepXSJ7dGPsh3CxBQ12rpMzYDHwngynNASN1hj6VXCG_0jAsppuQ)

  

![](https://lh6.googleusercontent.com/fBiQlo9Z6sJ0ZApy70FO5uCvRrmj3nFDo3HaCoQijzj562OGIfgHAiPCez2P0_n03bcPY23ZZrq2ATGfn3QxkGQ8AtGsPbax7UefwdcaK1ASRFrdtFRW-U5C7f_IHEWNmAHWtCkbOkmO3vMlSw)

Account of Manon is finally found.

  

Let’s wrap up the work for Samuel.

![](https://lh5.googleusercontent.com/XwvYc8gM0BItYZSp5wI1N66nF36OZ-sZvwk6boGkSpGYBSZqMNdXjNoWSKVJTJtrFhw-giK4GYc_LGCD3AKnh2Bo7nHuWUf6HIZ3Bh4-iw0_Z3ah_vwL5rp-JUrj6reYUm5xrFxTTV4JFmS_UA)

  

Let us now validate each reports.

![](https://lh4.googleusercontent.com/H79YRglXTYfnfK2PxXjunfmNAieXD2Rt17EdmAfhOdn4AoXeVWipnu04Xy2sI81fh3h9WWfEwJZ27PLbhVzO97PiOLFpRnlywq_izdji3O1rbIMsOJlkS-bypSNbB70qeVPLB-6o3YFCwZYhGQ)

  

Since all our work is validated. Let us now find the Admin credentials. For which we need to get a GET 200 request successful. Surfing through the networking tab under developer console we can get the instance of the request.

![](https://lh4.googleusercontent.com/t4HBHcl5PADoXReBXoUByiASoWA88skryS84LaGGrjUMb_C2TwZyUAjod9928jG1e_U_Dz8NfHxkFp5f81GXu_SEzNJTpluRmlIzn6-QZZ6Il-vld9Qtnx0rVO8BBDO7Jdoi_qEgcbzCL_mo6g)

  

Let us use SQL injection into the database using the GET requests and the User-Agent parameter.

![](https://lh5.googleusercontent.com/W3Q1D5h-Sl99e6AlLnADsZvfPFbyXfn7ErhkquN8b-tOp27oTioxges3X9C1b8d6ja7PvjZqRe1L0FUTGptwPK8p1z1byZ2NGQdbMpFfhL7wXTi5idiLEWLb5uoRmSGA5ZMxD2wL_MTbO-6Uzg)

  

Finally we need a payload to send in as a get request.

![](https://lh3.googleusercontent.com/QqsqszcQCd9kN1VMLGnlek0Iz_68dvYWSvXnpPTNF5MlhzXx-cQusmQ5bKcpTBWBrgmGwui2mxERejDeCWAhAIykHMRQf6FvxGGECKdOaA_ANEvO1S59heVTnzT7_7Zjr5sMPACV67CMUC3naA)

  

Using the Inspector tab we get to know that the admin has id=2 ![](https://lh4.googleusercontent.com/8Hh-TkdcwSyX6jTqL9ecm3v5vf4DsW8Yirrq4trlNeFyNMPJFXAtASNPRbb8DeTklk_mVcuTRjtbmRzuGifFkRGNucyVGIJ1BMvGTWZgsWi6IWCilBgbjoH6R-VldpFGw8DAmTr6VfGwm7MDZw)

  

Now all we need to do is run the exploit script.

![](https://lh6.googleusercontent.com/qiTgPOPifwihAE5YcSjUdVrxYGKWwJa2ClD6Q4Bx8i12nPz9Gigy4-9iG2drYX50lFH2rQj6ZRP647-EPUMICS_a52id3DtgrDPuXpDocskFRD24genfZbpINN_2NpQo0yaTYnBj_6zs2GJx0g)

  

After the script has completed the task we get the tables that we need in order to get admin credentials.

![](https://lh3.googleusercontent.com/1mmeQCF_I7pl0Era8nxS3Jid1X3xIEW1giqBbSD6jD1a_diOn0mGEdimt3ITGZZqOfznX3y-OIhoTjJppIOROe2r-mgRNA3r6-OLLKopuvhtNoW86ksI0ABg6ggkLDHdMPoQ_cLFNcZ13VtN9g)

The database of tables can be found under the account of Manon. (I forgot to take a screenshot but it is right there on the dashboard).

  

Now we need to run a specific command to drop the tables of the user credentials database. Using this payload below.

  

![](https://lh4.googleusercontent.com/WnObjrvCHUKGL3A0FdmZX0V7SOvHT-0sr6EVP9PYofSK5YaGG7jrzIdfCu3fFjTk2_vdLbaxJ1aNJT1f6Gd408pGtzvFADchx3W9AtuLrHzCYyYAWRNwmBY7PJVKOHvrr3Q6FRqRy2DlY_TkoQ)

  

Now as a result we get all user credentials. Just like that.

  

![](https://lh4.googleusercontent.com/Vf4bqCVwVSJ9-m8PguHCsJiNTo-xh2uvUE-3TfQRlnTqT7rc0Uxp6CC57zd2zqBacPbwJ6rXLI-dyVGzR6tKNiZaMWzjJUmFADh5Jxy8Xqs50x6t-u9DUgb3PQJfeARmT6gjwombC9g-ZxFtxg)

  

But there is one final step. All the users passwords are in hash format. For this we can either use HashCat, JohnTheRipper, HashCracker, HashDeep, but I am going to use Crack Station. Essentially any one is fine as long as it is working. I specifically use Crack Station due to habit. So, now let us copy the hash of Paul Baudouin since he appears to be the admin.

  

![](https://lh5.googleusercontent.com/jJjh3qBtzOublZEX0esUJx-WwnMnd5WqjPXXbCvtkfgLkBhhyBcInIJFEC4H07RZXQpM9O1gwItiQFH0Bz9OH5p3Xes_wLGw-GqNrqfpxwc5GylY1-iGddnwptJqOt9mMgK53rprbwU5CqTbhA)

  

So we can see that the password is HackMe and the hash format is md5.

So, let’s get our work done and login to get the flag.

USER: pbaudoin

PASS: HackMe

  

Login to admin was successful.

![](https://lh5.googleusercontent.com/FsH1oqTo67QCrWRQoAlbXdWtmTk__KfTs2Yx1RaZuJabofz3LoPh2C5hj6-wv2xh2K8Cgowzd8ygVz5XinGyAq7KYxB8xu03z_UxSSB4s0bKDVnlyd7mtBJcNNeIB67igN_05xu1sDwA2QzupA)

  

And here we get the flag{H4CKY0URL1F3}

![](https://lh5.googleusercontent.com/ISZnJeNyPZn_m7L18LI0dLpyFblA_G7UAxYPn8TD1_NS945yoJS7CUmOf-sE097lH4EWgRzjfg-Nznu84OBHCwuOX938x51h_I9zALV5-RvXxlupVcvBFj_l61Y9CIKW8WzgS4PJljxsB_Chgw)

Conclusion:

  

This VM contains a lot of challenges for us to Pen Test. Such as XSS attacks, Cookie stealing, Source code modification, SQL injection, php poisoning, Hash Cracking and Privilege Escalation. Overall this was a fun VM which took me a lot of time to solve. Initially I was unable to solve it due to my blank knowledge over cookie stealing. But since I was allowed to access the youtube I watched this video [https://www.youtube.com/watch?v=T1QEs3mdJoc](https://www.youtube.com/watch?v=T1QEs3mdJoc) of Cookie stealing by @Computerphile, which was of great help to me. Thanks a lot for reading my PoC on the VM on Vulnhub:

-   Name: MyExpense: 1
    
-   Date release: 7 Dec 2019
    
-   Author: [Sh4rpf0rc3](https://www.vulnhub.com/author/sh4rpf0rc3,662/)
    
-   Series: [MyExpense](https://www.vulnhub.com/series/myexpense,265/)
    

The link to this VM is present at the top of this PoC.

  

Thank you! Have a Hacky Day!