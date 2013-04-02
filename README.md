Simple utility that allows sharing of your desktop background

In the current version it only works for Macs and it requires Amazon S3 account, and a way to mount the S3 bucket to a directory in your machine.


1. First create a an amazon bucket with its own keys (here is howto https://gist.github.com/ogt/5294121). 
Name your bucket mydesktopbackground.mydomain.com.

2. Setup mountable access to that bucket (here is how to for Mac https://gist.github.com/ogt/5294262) 
so as ~/mydesktopbackground/s3 mounts to the s3 bucket

3. Install and run the utility 
```
> pip install git+git://github.com/ogt/mydesktopbackgroun.git
> # run once rigt away so as we can test it
> mydesktopbackground
> # add entry in crontab - or just use crontab -e to do it
> (crontab -l ; echo "@hourly mydesktopbackground") | crontab -
```

4. Test the utility

Confirm that the utitlity captured the file
```
> open ~/mydesktopbackground/s3/desktop.jpg
```
Confirm that the file is uploaded at amazon by opening your aws s3 console and confirming that the object is uploaded

5. Make your desktop publicly access
Assuming that you are interested in making your desktop publicy accessible
  - In Aws S3 console in the mydesktopbackground.mydomain.com bucket 
  - Right click desktop.jpg
  - Select permissions
  - Add Permission -> Everyone Download/Open

6. Copy the public link and open it in an incognito browser to confirm that you can access it anonymously

7. Use your desktop anywhere e.g. by pasting  it in a github home page markdown
```
[![MyDesktopBackground](http://...desktops public link..jpg)]
```

The utility will be overwriting the file everytime you change (within an hour if you set it an hourly cron job) and any referensed to the public link above will reflect the new background.


