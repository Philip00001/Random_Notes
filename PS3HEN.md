# Brewlogy, where the homebrew stuff are found
https://store.brewology.com/homebrew.php?category=Apps&orderby=

# Playing games of older/legacy system
Check [[PS3RetroArch]] for details.

# Installing PS3 games
Check [[PS3Rom]] for details.

# Transferring Files with FTP
https://consolemods.org/wiki/PS3:Transferring_Files_with_FTP
- **Note**: using direct connection to the router gives a 11MB/s instead of 1.2~1.5 MB/s from [[webMAN]] and <2.5MB/s from [[multiMAN]]
- **Recommendation**:  for any >1 Gb files, try direct connection when possible
- **WARNING**: deleting files from FTP **DOES NOT RELEASE SPACE!**, use mmCM to move files/delete them
Side notes: [[webMAN]] speed are sometimes faster when playing, up to 2MB/s, but its not guarantee to be stable.
# Recommended download
- Unofficial_multiMAN_04.84.00_BASE_(20190528)_[PS3HEN]_fix-info.pkg.453.v4.84_HEN_brewology_com.pkg
- webMAN_MOD_1.47.48_Installer.pkg.530.v1.47.48n_brewology_com.pkg
- apollo-ps3.pkg.286.v2.2.4_brewology_com.pkg
- sfm_ps3.pkg.222.v0.5.2_brewology_com.pkg
- ArtemisPS3-GUI.pkg.434.vr6.4_brewology_com.pkg

# Playing PS2 games

## Choosing the Right Game
Check [PS2_Classics_Emulator_Compatibility_List](https://www.psdevwiki.com/ps3/PS2_Classics_Emulator_Compatibility_List) for accurate, up to date info.
You should avoid games with issues unless you like to deal with it.

## Prerequisite (Install ***in order***)
- [[webMAN]] MOD (Which you should have)
- PS2 Classics Launcher (Located in webMAN MOD)
- PS2 CONFIG Database (Located in webMAN MOD)
- mmCm (AKA [[multiMAN]])
## Process
1. Install the stuffs listed above
2. Transfer your PS2 game to PS2ISO folder
3. Check if the game are .BIN.ENC, IF YES, GOTO step 14
4. IF NOT, use mmCM and boot into multiMAN mode
5. Goto Retro under XMB layout
6. Press X button on the game to turn them into PS2 Classic
7. Goto mmOS
8. Move into PS2ISO
9. You should be able to see new folder, named after the game you chose
10. Move into the folder, Rename the only file into to "Your_Game_Name.ISO.BIN.ENC" (Or anything you like)
11. Cut and move the file to the parent folder (PS2ISO)
12. Remove the PS2ISO left behind (Optional)
13. Quit mmCM
14. Refresh XMB and games with webMAN
15. Now load the game under PS2ISO
16. NOTHING will pop up, it is normal
17. Open PS2 Classic Placeholder, if should be in the bottom if you have never use it before
18. Play the game, note that the virtual memory card is in PS2 Classic Placeholder, not in the system one

### Misc
https://www.psx-place.com/threads/so-i-installed-ps3hen-without-activating-my-psn-account-am-i-screwed.42081/