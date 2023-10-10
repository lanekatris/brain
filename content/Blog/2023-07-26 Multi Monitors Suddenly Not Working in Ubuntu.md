Sometimes Ubuntu 22.04 breaks when I put it to sleep. It sometimes has to repair the file system as well.

This recently happened, and as I hard rebooted I saw only one monitor was working. Having now idea what was going on I Googled and found:

https://www.reddit.com/r/Ubuntu/comments/uy7k70/ubuntu_2204_wont_recognize_2nd_monitor/

The first comment about a *video driver*...

So I checked, low and behold, my video driver was not being used. I chose the latest and greatest Nvidia proprietary driver and now I'm good to go 🤷