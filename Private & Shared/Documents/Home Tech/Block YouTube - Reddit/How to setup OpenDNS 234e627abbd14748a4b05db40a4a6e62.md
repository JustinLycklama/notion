# How to setup OpenDNS

To block youtube or other sites from wifi, I'm using Opendns.com

Setting this up will be the trickiest part, as I have not done it recently and the instructions will differ depending on your router.

[https://www.opendns.com/setupguide/](https://www.opendns.com/setupguide/)

You can try to find you listed router above, or I'll make a generic instruction here

### **Step 1. Connect to your router from your browser**

You can connect to your router through its ip address in your browser. For example, to access my home one I go to[http://192.168.2.1/](http://192.168.2.1/)To find your ip address, follow these steps[https://nordvpn.com/blog/find-router-ip-address/](https://nordvpn.com/blog/find-router-ip-address/)

### **Step 2. Login**

Once you can see your router's page, you'll need to sign in. The username and password should be written directly on your router.

### **Step 3. Enter DNS information**

The goal here is to have our router ask OpenDNS for addresses to websites.

Find the DNS section in your router's advanced settings, select manually specify, and enter OpenDNS's information

- 208.67.222.222
- 208.67.220.220

### **Step 4. Create an OpenDNS account**

Just sign up here

[https://dashboard.opendns.com/settings/](https://dashboard.opendns.com/settings/)

### **Step 5. Download their software**

Once you are signed up, download the software on a computer and allow it to auto start when you start your computer. This will help link OpenDNS with your home address.

Look for this message.

### **Step 6. Blocking Content**

You should now be set up with OpenDNS! Nothing should behave differently, but your router is using OpenDNS as a middleman between you and internet traffic.

To block some content, click on the IP button of your network

Now you will be presented with a page for Web Content Filtering

Add the urls you want blocked to the individual domain list to block the site. It will take ~5 mins to take effect.

### Specific Domains

Youtube specifically comes from multiple sources. You can go to

[youtube.com](http://youtube.com/)

, but videos also get embedded in other pages, you could use an app on your phone, you could use your tv...

This is the complete list right now

### Youtube

- [googlevideo.com](http://googlevideo.com/)
- [youtu.be](http://youtu.be/)
- [youtube-nocookie.com](http://youtube-nocookie.com/)
- [youtube.com](http://youtube.com/)
- [youtube.googleapis.com](http://youtube.googleapis.com/)
- [youtubei.googleapis.com](http://youtubei.googleapis.com/)
- [ytimg.com](http://ytimg.com/)
- [ytimg.l.google.com](http://ytimg.l.google.com/)