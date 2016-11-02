Armadillo 3.xx 4.xx 5.xx 6.xx 7.xx Unpack.txt

This script is for most armadillo protected apps, using standard protection, iat elimination, debug blocker, code splicing, disable thread monitoring, advanced import elimination or any combination there of. Your target must not use CopyMemII or have Memory Patching Protection enabled. This script also fixes and logs Imports to ArmAccess.dll. It also detects Secured Sections and reports how many if present (this will be different depending on if registered or not).

Armadillo 3.xx 4.xx 5.xx 6.xx Detach+CopyMemII.txt

This script is for detaching an armadillo with CopyMemII, I have written a new one because it did not work properly with some older 3.xx versions of Armadillo. This one works with Armadillo 3.xx 4.xx 5.xx and 6.xx.

Armadillo 6.xx 7.xx Detach+CopyMemII.txt

This script is for detaching an armadillo with CopyMemII, it is only for later version of 6.xx and v7.xx versions as some extra anti-debug was added to these versions.

Armadillo 3.xx 4.xx 5.xx 6.xx 7.xx CopyMemII Debug Blocker IAT Recover.txt

Use this script after detaching with Armadillo 3.xx 4.xx 5.xx 6.xx 7.xx Detach.txt Script, it will automatically fix IAT redirection and redirect and recover ArmAccess.dll (Security.dll internal) calls before landing on false OEP.  It also detects Secured Sections and reports how many if present and logs them (these will be different depending on license level).

Armadillo 3.xx 4.xx 5.xx 6.xx 7.xx Detach.txt

This script detaches Parent from Child. If Armadillo 3.xx 4.xx 5.xx 6.xx 7.xx CopyMemII+Debug Blocker IAT Recover.txt Script hangs after asking armadillo version, run it again. (bug in olly script???)

Armadillo Version is just a little script to get exact version from your target. It supports 3.xx to 7.xx and Debug Blocker/CopyMemII.

I have also included a patched ArmAccess.dll for your use.

Note A: With the CopyMemII and Detach scripts, sometimes olly won't resume the thread. If this happens, just open the thread window, right click the thread, and choose resume. You may have to resume it LOTS of times before it finally resumes, but it will eventually. (Bug in olly?)

Note B: On newer versions of arma (5.xx-7.xx) when using the Detach Script, you must leave olly open after detaching, and attach the child process with a fresh instance of olly, because it checks for which mutex opened the child.

Note C: Sometimes dll unpacking fails because the code takes a different path (4.66 and maybe others), in which case say YES to the secure section fail query.

Note D: Why 2 different ArmAccess and one with different name? The Unpack and IAT recover scripts now fix SDK calls outmatically. Put the ArmAcces!.dll into the installation directory. After rebuilding imports change the ASCII name in the IAT back to ArmAccess.dll and distribute that one with your work.

Note E: Scripts will not work with certain versions, For Ex 4.99Alpha, sorry but they are so different and so rare it's not practical to add compatibility for these versions. You'll just have to unpack them manually.

Note F: When an overlay is detected, sometimes it might just be crap (CopyMemII). Real overlays generally start at membase+0x20.

New Stuff:

IAT Redirection is now more intelligent.
Added Armadillo v6.xx/7.xx compatibility.
Secure Section checking is now more intelligent.
Added patching for the thunk seperator, no more invalid thunks!
ArmAccess SDK API checking is now more intelligent.
Compatibility with a wider range of targets (all versions).
Overlay detection, logging, and dumping.
ArmAccess SDK API automatic fixing, no more fixing by hand!
UPX detection and OEP finder.
ArmAccess.dll updated
Version Detection Script

To Do:

Hardware ID patching.
Section Name Decryption Script.

Final Note:

Only tested on WinXP SP3, Vista/Win7 (32bit) testing would be appreciated.

Special Thanks

Sunbeam and LCF-AT for ideas and/or testing.

Cheers!