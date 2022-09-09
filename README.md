# FloppySwitchBoard - Alpha

The Floppy Switch Board 
is designed to allow you to connect multiple (theoretically indefinite) floppy drives to
a single drive interface by letting you manually switch between them.

## How it works

Floppy drives using the Shugart drive interface have 4 ID wires that are used to identify the 
drives which are all connected to the same physical cable. When a floppy controller requests 
data from a floppy drive, the signals are sent to all connected drives. But only the drive
with the correct ID will respond. Each drive is configured, in some way, to have a unique ID.

The floppy Switch Board allows you to take one physical connector and connect two drives to 
it. It then intercepts and redirects the ID signal to one of the two drives using a switch.

## Compatibility

I just barely had these first batch of alpha prototype boards in and then unfortunately had 
to move. So my testing has been cut short in this area until I can get set back up to 
continue.

The board design as is should be compatible with at least IBM PC drive interfaces. The 
current revision of the board here switches not only the ID line but also the motor control
line which is needed for PCs. Unfortunately this is incompatible with pure shugart spec 
systems like the TRS-80s. I need to make a revision of the board that allows you to 
add/remove a jumper for switching the motor power line for PCs so it can be used with
more systems.

## Usage

Being a completely passive device the floppy switch board does not require drivers or 
software of any kind to work, but it can benefit from it which I will cover in a 
moment. The most simple setup would be connecting two drives to the system for use
with disk imaging software that directly controls the drive such as IMD or dskImage.
Drives connected to the board itself must use *non*-twisted cables. Additionally
because it switches the ID and motor lines it needs a DPDT switch for both signals
which I have not yet found a prewired solution for. So you will have to get a switch
and wire to put one together yourself.

For normal DOS use there is a more advanced configuration that can be done using 
`driver.sys`. There is [some](https://web.archive.org/web/20210412134354/http://info.wsisiz.edu.pl/~bse26236/batutil/help/DRIVER_S.HTM) documentaion on its features that allows you to manually
create new "virtual" floppy drives on an MS-DOS system. It is even smart enough to
know when you have multiple drives connected to the same ID to give you a moment to
confirm that the drive is ready. With `driver.sys` you can switch between both drives 
connected to the floppy switch board almost as if they were connected directly to the 
drive controller. It doesn't work with software that accesses drives directly though 
and doesn't work well with software that doesn't run on the command line. I don't have
time at the moment to write out a full guide on the usage of it and the one website I
found that detailed it will is gone and I forgot where it was. I will update this with
both a link and a full tutorial on it when I have the time.

The Floppy Switch Board can be used on a Windows system but it is not easy and to there
are issues. The `driver.sys` feature was removed in Windows DOS versions and I cannot
find an alternative feature to replace it. Since Windows uses the BIOS configuration 
for the floppy drives it will only ever have the drives you tell it exist there. Even 
if you connect two similar drives (such as two 1.44MB) Windows will not refresh the
ToC that lists the files on the disk in a way you expect which can make it difficult to
use. I need to do more testing to charactarize how this works and see if there is a 
solution. Imaging programs that directly access the hardware should still work though.

## Gotek?

Yes, this works with a Gotek! This is probably the easiest use for it because you will
most likely be using the Gotek to emulate the same type of drive you already have 
connected. By placing the floppy switch board in front an existing traditional floppy
drive you connect both it and the Gotek to a system and keep both usable(Keep in mind 
potential commpatibility issues because of the PC drive motor line though). 

## Roadmap
I will be updating this project and continuing development on it once I have settled in
to my new office. I have multiple things I need to correct on it before I am going to
call it done. I need to fix the following for the beta version:

 - Add jumper for motor select and possibly redo ID signalling entirely to support non-pcs
 - Changing mounting holes to match *something* on a floppy drive to make it easier to install


