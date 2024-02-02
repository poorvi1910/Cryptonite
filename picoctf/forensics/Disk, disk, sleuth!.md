I unzipped the file and obtained a file dds1-alpine.flag.img.</br>
Running srch_strings on the file to display printable strings in a file.</br></br>
( **NOTE:** strings is a GNU tool that looks for potential ASCII and unicode strings inside binary content. srch_strings is part of sleuthkit, does exactly the same thing, but can also print the offset at which a string was found.)
</br></br>
But this gives us a seemingly never ending list. hence piping it thorugh grep we execute the following command: </br>
srch_strings -a dds1-alpine.flag.img | grep pico </br>

This displays the following output: </br>
ffffffff81399ccf t pirq_pico_get</br>
ffffffff81399cee t pirq_pico_set</br>
ffffffff820adb46 t pico_router_probe</br>
  SAY picoCTF{f0r3ns1c4t0r_n30phyt3_dcbf5942}</br>
</br>
Flag: picoCTF{f0r3ns1c4t0r_n30phyt3_dcbf5942}
