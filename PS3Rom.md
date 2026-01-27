https://myrient.erista.me/files/Redump/Sony%20-%20PlayStation%203%20-%20Disc%20Keys%20TXT/
Need both .key, .dkey (.key for playing iso and decrypt on the fly, .dkey for decryption on the computer)
Note: ps3hen somehow failed to use the .key file, try [[#To use ps3dec]].
(Use Free Download Manager or others alternative to speed up download)

Roms downloaded from here need to be first decrypted to be play.
https://github.com/Redrrx/ps3dec
## To use ps3dec :
Make a /keys folder in the same path as the executable, the --auto option will find the .dkeys by name automatically.
```sh
 ./target/release/ps3decrs "$(fzf)" --auto --tc 64
```
# Decrypting PS3 ISOs
https://consolemods.org/wiki/PS3:Decrypting_PS3_ISOs

# About games with 2 disks
I came across [[Biohazard 5]] with have a disk call alternate version/gold edition, thought it would be a standalone disk. I was far off, turns out you need both disk/iso installed to play it
