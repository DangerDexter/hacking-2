#对5分钟原则的重新思考

for 《中国计算机学会通讯》

#解释5分钟原则

#从<https://pcpartpicker.com/trends/>分析

DDR3-1600 204-pin SODIMM 2x8GB
140/(16.0) = $8.75/G

SSD - 512GB
360/(512.0) = $0.703125/G

Hard Drive - 4TB - 7200 RPM
260/(4.0*1024) = $0.0634765625/G

#架构的演化


>以下摘录自Jim Gray《Transaction Processing》1992版

##Transaction Processing p56-57
###The Five-Minute Rule
How shall we manage these huge memories? The answers so far have been clustering and sequential access. However there is one more useful technique for managing caches, called the five-minute rule. Given that we know what the data access patterns are, when should data be kept in main memory and when should it be kept on disk? The simple way of answering this question is, *Frequently accessed data should be in main memory, while it is cheaper to store infrequently accessed data on disk*. Unfortunately, the statement is a little vague: What does frequently mean? The five-minute rule says frequently means five minutes, but the rule reflects a way of reasoning that also applies to any cache-secondary memory structure. In those cases, depending on relative storage and access costs, frequently may turn out to be milliseconds, or it may turn out to be days(see Equation 2.7).

The logic for the five-minute rule goes as follows: Assume there are no special response time(real-time) requirements; the decision to keep something in cache is, therefore, purely economic. To make the computation simple, suppose that data blocks are 10 KB. At 1990 prices, 10 KB of main memory cost about $1. Thus we could keep the data in main memory forever if we were willing to spend a dollar. But with 10 KB of disk costing only $.10, we presumably could save $.90 if we kept to 10 KB on disk. In reality, the savings are not so thing. How much, then, does a disk access cost? A disk, along with all its supporting hardware, costs about $3,000(in 1990) and delivers about 30 accesses per second; access per second cost, therefore, is about $100. At this rate, if the data is accessed once a second, it cost $100.10 to store is on disk(disk storage and disk access costs). That is considerably more than the $1 to store it in main memory. The break-even point is about on access per 100 seconds, or about every two minutes. At that rate, the main memory cost is about the same as the disk storage cost plus the disk access costs. At a more frequent access rate, disk storage is more expensive. At a less frequent rate, disk storage is cheaper. Anticipating the cheaper main memory that will result from technology changes, this observation is called the five-minute rule rather than the two-minute rule.

###The five-minute ruls: 
Keep a data item in electronic memory if its access frequency is five minutes or higher, otherwise keep it in magnetic memory.

Similar arguments apply to objects stored on tape and cached on disk. Given the object size, the cost of cache, the cost of secondary memory, and the cost of accessing the object in secondary memory once per second, frequently is defined as a frequency of access in units of accesses per second (a/s):

Frequentcy ≈ 

Objects accessed with this frequency or higher should be kept in cache.

###Future Memory Hierarchies
These are two contrasting views of how memory hierarchies will evolve. The one proclaims *disks forever*, while the other maintains that *disks are dead*. The disks-forever group predicts that there will never be enough electronic memory to hold all the active data; future transaction precessing systems will be used in applications such as graphics, CAD, image processing, AI, and so forth, each of which requires much more memory and manipulates much larger object that do classical database applications. Future databases will consist of images and complex objects that are thousands of times larger than the records and blocks currently moving in the hierarchy. Hence, the memory hierarchy traffic will grow with strict response time constraints and increasing transfer rate requirements. Random requests will require the fast read access times provided by disks, while the memory architecture will remain basically unchanged. Techniques such as parallel transfer(striping) will provide needed transfer rates.

The *disk-are-dead* view, on the other hand, predicts that future memory hierarchies will consist of an electronic memory cache for tape robots. This view is based on the observation that the price advantage of disks over electronic memory is eroding. If current trends continue, the cost/byte of disk and electronic memory will intersect. Moore's Law(Equation 2.2) "intersects" Hoagland's Law(Equation 2.4) sometine between the years 2000 and 2010. Electronic memory is getting 100 times denser each decade, while disks are achieving a relatively modest tenfold density improvement in the same time. When the cost of electronic memory approaches the cost of disk memory, there will be little reason for disks. To deal with this competition, disk designers will have to use more cheap media per expensive read-write head. With more media per head, disks will have slower access times-in short, they will behave like tapes.

The disk-are-dead group believes that electronic memories will be structured as a hierarchy, with block-addressed electronic memories replacing disks. These RAM disk will have battery or tape backup to make them non-volatile and will be large enough to hold all the active data. New information will only arrive via the network or through real-world interfaces such as terminals, sensors, and so forth. Magnetic memory devices will be needed only for logging and archiving. Both operations are sequential and often asynchronous. The primary requirement will be very high transfer rates. Magnetic or magneto-optical tapes would be the ideal devices; they have high capacity, high transfer rates, and low cost/byte. It is possible that these tapes will be removable optical disks, but in this environment they will be treated as fundamentally sequential devices.

The conventional model, disks forver, is used here if only because is subsumes the no-disk case. It asks for fast sequential transfers between main memory and disks and requires fast selective access to single objects on disk.

