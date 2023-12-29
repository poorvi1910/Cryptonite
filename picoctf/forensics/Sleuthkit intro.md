We need to use mmls to find the size of the linux partition. So first we decompress the file using gzip and then run the decompressed file through mmls and input the answer to the netcat command

└──╼ $gzip -d disk.img.gz

└──╼ $mmls disk.img
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors


Slot      Start        End          Length       Description
      
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)

001:  -------   0000000000   0000002047   0000002048   Unallocated

002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)


└──╼ $nc saturn.picoctf.net 64605
What is the size of the Linux partition in the given disk image?
Length in sectors: 0000202752
0000202752
Great work!
picoCTF{mm15_f7w!}


flag: picoCTF{mm15_f7w!}
