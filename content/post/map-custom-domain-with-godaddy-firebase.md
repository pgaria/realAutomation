---
title: "Google Firebase custom domain mapping with GoDaddy"
date: 2017-11-28
draft: false
description: "How to Map your custom domain in FireBase with GoDaddy instructions."
categories: [ "Web Hosting", "Google Firebase"]
tags: [
    "Web Hosting","Google Firebase","Custom Domain"
]
---
In my [last post](https://www.pawangaria.com/post/deployyourwebsiteonfirebase), I explained about hosting our website on Google Firebase and we are able to access the website using the firebase Url. Now in this article, we are going to talk and learn about adding our website with custom domain like your own domains purchased on the domain providing websites like [GoDaddy](https://www.godaddy.com/) and [NameCheap](https://www.namecheap.com/). 
I this article we are going to integrate our domain in GoDaddy with Firebase hosted website. I tried and Integrated my custom domain by taking reference from this [documentation](https://firebase.google.com/docs/hosting/custom-domain)

Step 1: Go to firebase console and check your project. 
![Firebase console](/img/customDomain/projectHomeFireBase.png)

Step 2: Click **Hosting** Link from the left side and you can see your default website deployed.
![Hosting link](/img/customDomain/hostingProjectPageAfterDeploy.png)

Step 3: Click **Connect Domain** link from the page.

Step 4: Add Domain name in the connect domain popup.
![Add Domain name](/img/customDomain/domainNamePopup.png)
 
Step 5: Now you will get the google site verification ID and Copy the Id
Note: Do not copy the only value, you should copy the whole text like:

 **google-site-verification=9xUIjWlRgKX-jsM8Hhlaj3HHtDK0xnEoA98Ms** 

We need this google site verification Id to add to **TXT** record in DNS provider.
![Add google site](/img/customDomain/verifyOwnershipVerificationId.png)

Step 6: Now go back to GoDaddy and login to your account and go to [Domain Page](https://dcc.godaddy.com/domains/)

Step 7: Now click on the three dots near to **Use My Domain** button and click **Manage DNS** link.
 ![click use domain](/img/customDomain/manageDomainDnS.png)

Step 8: On manage DNS page add the value of google site verification Id as TXT value in the list.
 ![Add TXT value in DNS](/img/customDomain/TXTvalueforGoogleVerification.png)

Step 9: Now after adding this **TXT** value in the DNS list, Go back to firebase console and click the verify link from the custom domain popup.

Step 10: In FireBase on GoOnline Step you will get 2 IP address which you need to add in the GoDaddy DNS table again as **Type A** value.
 ![Add IP address as A value](/img/customDomain/typeAvalueinDNStable.png)
 
Step 11: Now go back to Firebase console again and Connect.

After performing all the steps in  some time, you can see your website is up and running with the custom domain you just added in the firebase.
** You will see certificate error for HTTP for some time but after some time with certificate verification, the error will go and you can access website in HTTPS**

Above steps, I used to connect my custom domain with GoDaddy and It worked for me. I wrote this article because I didn't find any recently updated article on the internet about the whole process. 

Feel Free to write me If you feel any issue with your custom domain.

Thanks for reading!
