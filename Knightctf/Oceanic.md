I first used exiftool on the jpeg and found a comment there which looked encoded. Running it through a cipher decoder, it is revealed to be base58 encoded

![o1](https://github.com/poorvi1910/Cryptonite/assets/146640913/887db826-d874-4aa4-a740-33f1869f33be)

The code reveals: "theoceanisactuallyreallydeeeepp"

The emphasis on the word deep leads us to a steganography tool called DeepSound. Running the .wav file through deepsound, it gives out a 'flag.png' file. The picture itself does not reveal anything. But running the strings method on the picture gives us the flag. 

Flag: KCTF{mul71_l4y3r3d_57360_ec4dacb5}
