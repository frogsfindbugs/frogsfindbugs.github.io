## Analysis of a Fraud Android App - Jio Prime

##### TLDR: A fake crypto-currency mining app, named Jio Prime, was being marketed over Instagram pages. This Android app used the UI similar to Jio's original apps and tried to conceive users to install the app and later stealthily mine cryptocurrency on their devices.

I am following an Instagram page with about 130K followers. These pages post ads sometimes when they get paid for them. One such ad said – “Get 10GB Data Everyday for Free for 3 Months – for Jio Prime Users”. Since I am a Jio user, I got curious to check this and was sure – this was some kind of fraud going on, and the ad was not by original Jio — they were using the name of Jio to milk their followers, since many of the users use Jio for their data connection.

I visited the URL (link) and downloaded the mentioned APK (JioPrime.apk), which is hosted on Google Drive. Turned-on the emulator and loaded this APK – yes, the icon was same as Jio’s logo (spot the app named Jio Prime in screenshot below). On opening the APK, it gives look-n-feel similar to MyJio app (the self-service app for Jio customers):

photos ============

It asked me to provide my phone number. I started capturing the request/responses with Burp to look for anything malicious – I entered my mobile number and it gave me the loading screen, saying something is happening in the backend. Any user will be convinced by the different pop-ups saying: ‘Connecting to Sever…’, ‘Connected’, ‘Activating Offer’. Next it took me to “Share with Whatsapp” screen, where it asked me to share it with 10 users on Whatsapp.

photos ============

But there were no network connections till that point, and then it started sending some data to Google Adwords URL.
Next, I entered mobile number as 0000000000, and it still accepted my mobile number as valid Jio number and showed me the loading pop-ups, next with the Share on Whatsapp screen. Since I don’t have Whatsapp installed on the emulator, I was not able to test further, but I was sure that they were sending user clicks to Google Adwords.

##### The [MobSF](https://github.com/MobSF/Mobile-Security-Framework-MobSF) analysis results are here: 

1. Some of the dangerous Android permissions asked by the app:
a. READ_EXTERNAL_STORAGE
b. WRITE_EXTERNAL_STORAGE
c. READ_SMS
d. ACCESS_FINE_LOCATION
e. SYSTEM_ALERT_WINDOW

2. Below is the list of malicious URLs and Domains contained in the APK. When you “Share via Whatsapp”, your contact will receive the link like “Activate this service before*\n*12:00AM Tonight to Enjoy*\n*25GB/Per Day!!*\n\n*Team Jio.*\n\n*Link* : http://tiny.cc/Jio-Free-1Year“;“

photos ===============

Later I uploaded the APK to [VirusTotal](https://www.virustotal.com/gui/home/upload) for their analysis. One thing that attracted my attention was a Service named “er.upgrad.jio.jioupgrader.Coinhive“. While Coinhive (link to KrebsonSecurity article) is a cryptocurrency mining service, this app could be a miner in the name of Jio. Eat the process of user device, earn money for the APK owner.

Ten (10) Engines at VirusTotal also marked this app as malicious, screenshot here:

photos ===============

##### Takeaways:

I could just see their JioPrime ad on 1 page on Instagram, but not sure where else they have posted their ads and how many victims have installed their APK. Also, since the app is having dangerous permissions (like Read & write external storage, read SMS), I am sure they would be accessing and sending this data somewhere.

It is highly recommended not to install APKs from unknown sources. Even some of the Google Playstore apps have malwares in them, but that’s totally a different topic.

##### To-do:

– Check if it is mining any cryptocurrency
– Reverse Engineer the APK for finding out the creator of the APK and the relevant Adwords account
– Check if it is really not making any network connections other than the Adwords part
– What data from user device is being accessed, whether it is being sent anywhere

In case you have free time, please feel free to do further analysis of the APK and provide more malicious vectors.

- You can download the APK from this blog: [http://jiodatapack.blogspot.com/]
- VirusTotal report available here: [https://www.virustotal.com/#/file/7f4cea3b6bceb4aebb45a8f1c6e528f90eec1a87009f18d93de51b32fc85034c/detection]
