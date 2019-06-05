-------------------------------
OllyScript plugin v0.62 by SHaG
-------------------------------

1. About OllyScript
2. Status
2.1 What's new in v0.62?
3. Documentation
3.1 Language
3.2 Labels
3.3 Comments
3.4 Menus
4. Contact me
5. License
6. Thanks!

------------------------------

1. About OllyScript
-------------------
OllyScript is a plugin for OllyDbg, which is, in my opinion, 
the best application-mode debugger out there. One of the best 
features of this debugger is the plugin architecture which allows 
users to extend its functionality. OllyScript is a plugin 
meant to let you automate OllyDbg by writing scripts in an 
assembly-like language. Many tasks involve a lot of repetitive 
work just to get to some point in the debugged application. By 
using my plugin you can write a script once and for all. 

------------------------------

2. Status (4 March 2004)
----------------------------
Fixed another hardware breakpoint bug (thanks loveboom).
Also added ability to change the EFLAGS register (see the MOV command and section 3.1).

2.1 What's new?
---------------
The internal architecture of the plugin totally redone and object-oriented 
(its not perfect OO, but bear with it). Because of this rewrite, bugs are
likely to appear. Please report them to me ASAP!
Bugs with script processing are fixed, parts of code are redone etc.

+ New commands: 
	BPCND, BC, BPMC, JA, JB, JAE, JBE, AI, AO, TI, TO
+ Conditional breakpoints
+ Breakpoint clearing (even memory)
+ Tracing and animation
+ More jumps
+ Can change EFLAGS register
# BP behaviour fixed (it now SETS breakpoint, instead of TOGGLEING it).
# Bugs in script processing fixed (thanks s0nkite).
# LOG now logs things like strings that are referenced by the address,
  referenced function addresses etc. Try it, its cool!
# EOB now works correctly with hardware breakpoints.
# "Thanks" section of readme updated. =)
------------------------------

3. Documentation
----------------
Two example scripts (tElock098.osc and UPX.osc) are available with this release. 
The scripts will when run immediately find the OEP packed executable. 

3.1 Language
------------
The scripting language of OllyScript is an assembly-like language.

In the document below, src and dest can be (unless stated otherwise):
 - Constant in the form of a hex number withot prefixes and suffixes (i.e. 00FF, not 0x00FF or 00FFh)
 - Variable previously declared by VAR
 - A 32-bit register (one of EAX, EBX, ECX, EDX, ESI, EDI, EBP, ESP, EIP). Non 32-bit registers are not supported at
   the moment, but you can use SHL/SHR and AND to get their values.
 - A memory reference in square brackets (i.e. [401000] points to the memory at address 401000, [ecx] points to the memory at address ecx).
 - A flag with an exclamation mark in front (one of !CF, !PF, !AF, !ZF, !SF, !DF, !OF)

The following commands are available at the moment:

ADD dest, src
-------------
Adds src to dest and stores result in dest
Example: 
	add x, 0F
	add eax, x
	add [401000], 5

AI
--
Executes "Animate into" in OllyDbg
Example:
	ai

AND dest, src
-------------
ANDs src and dest and stores result in dest
Example: 
	and x, 0F
	and eax, x
	and [401000], 5

ASM addr, command
-----------------
Assemble a command at some address
Example:
	asm eip, "mov eax, ecx"

AO
--
Executes "Animate over" in OllyDbg
Example:
	ao

BC addr
-------
Clear unconditional breakpoint at addr.
Example:
	bc 401000
	bc x
	bc eip

BP addr
--------
Set unconditional breakpoint at addr.
Example:
	bp 401000
	bp x
	bp eip

BPCND addr, cond
----------------
Set breakpoint on address addr with condition cond.
Example:
	bpcnd 401000, "ECX==1"
	
BPMC
----
Clear memory breakpoint.
Example:
	bpmc

BPHWC addr
----------
Delete hardware breakpoint at a specified address
Example:
	bphwc 401000
	
BPHWS addr, mode
----------------
Set hardware breakpoint. Mode can be "r" - read, "w" - write or "x" - execute.
Example:
	bphws 401000, "x"

BPRM addr, size
---------------
Set memory breakpoint on read. Size is size of memory in bytes.
Example:
	bprm 401000, FF

BPWM addr, size
---------------
Set memory breakpoint on write. Size is size of memory in bytes.
Example:
	bpwm 401000, FF

CMP dest, src
-------------
Compares dest to src. Works like it's ASM counterpart.
Example: 
	cmp y, x
	cmp eip, 401000

CMT addr, text
--------------
Inserts a comment at the specified address
Example:
	cmt eip, "This is the entry point"

EOB label
---------
Transfer execution to some label on next breakpoint.
Example:
	eob SOME_LABEL

EOE label
---------
Transfer execution to some label on next exception.
Example:
	eob SOME_LABEL

ESTI
----
Executes SHIFT-F7 in OllyDbg.
Example:
	esti

ESTO
----
Executes SHIFT-F9 in OllyDbg.
Example:
	esto

FINDOP addr, what
-----------------
Searches code starting at addr for an instruction that begins with the specified bytes. 
When found sets the reserved $RESULT variable. $RESULT == 0 if nothing found.
Example:
	findop 401000, #61# // find next POPAD

GPA proc, lib
-------------
Gets the address of the specified procedure in the specified library.
When found sets the reserved $RESULT variable. $RESULT == 0 if nothing found.
Useful for setting breakpoints on APIs.
Example:
	gpa "MessageBoxA", "user32.dll" // After this $RESULT is the address of MessageBoxA and you can do "bp $RESULT".

GMI addr, info
--------------
Gets information about a module to which the specified address belongs.
"info" can be MODULEBASE, MODULESIZE, CODEBASE or CODESIZE (if you want other info in the future versions plz tell me).
Sets the reserved $RESULT variable (0 if data not found).
Example:
	GMI eip, CODEBASE // After this $RESULT is the address to the codebase of the module to which eip belongs

JA label
--------
Use this after cmp. Works like it's asm counterpart.
Example:
	ja SOME_LABEL

JAE label
---------
Use this after cmp. Works like it's asm counterpart.
Example:
	jae SOME_LABEL

JB label
--------
Use this after cmp. Works like it's asm counterpart.
Example:
	jb SOME_LABEL

JBE label
---------
Use this after cmp. Works like it's asm counterpart.
Example:
	jbe SOME_LABEL

JE label
--------
Use this after cmp. Works like it's asm counterpart.
Example:
	je SOME_LABEL

JMP label
---------
Unconditionally jump to a label.
Example:
	jmp SOME_LABEL

JNE label
---------
Use this after cmp. Works like it's asm counterpart.
Example:
	jne SOME_LABEL

LBL addr, text
--------------
Inserts a label at the specified address
Example:
	lbl eip, "NiceJump"

LOG src
-------
Logs src to OllyDbg log window.
If src is a constant string the string is logged as it is.
If src is a variable or register its logged with its name.
Example:
	log "Hello world" // The string "Hello world" is logged
	var x
	mov x, 10
	log x // The string "x = 00000010" is logged.

MOV dest, src
-------------
Move src to dest.
Src can be a long hex string in the format #<some hex numbers>#, for example #1234#.
Remember that the number of digits in the hex string must be even, i.e. 2, 4, 6, 8 etc.
Example: 
	mov x, 0F
	mov y, "Hello world"
	mov eax, ecx
	mov [ecx], #00DEAD00BEEF00#
	mov !CF, 1
	mov !DF, !PF	

MSG message
-----------
Display a message box with specified message
Example:
	MSG "Script paused"

OR dest, src
-------------
ORs src and dest and stores result in dest
Example: 
	or x, 0F
	or eax, x
	or [401000], 5

PAUSE
-----
Pauses script execution. Script can be resumed from plugin menu.
Example:
	pause

RET
---
Exits script.
Example:
	ret

RTR
---
Executes "Run to return" in OllyDbg
Example:
	rtr

RTU
---
Executes "Run to user code" in OllyDbg
Example:
	rtu

RUN
---
Executes F9 in OllyDbg
Example:
	run

SHL dest, src
-------------
Shifts dest to the left src times and stores the result in dest.
Example:
	mov x, 00000010
	shl x, 8 // x is now 00001000

SHR dest, src
-------------
Shifts dest to the right src times and stores the result in dest.
Example:
	mov x, 00001000
	shr x, 8 // x is now 00000010

STI
---
Execute F7 in OllyDbg.
Example:
	sti

STO
---
Execute F8 in OllyDbg.
Example:
	sto

SUB dest, src
-------------
Substracts src from dest and stores result in dest
Example: 
	sub x, 0F
	sub eax, x
	sub [401000], 5

TI
--
Executes "Trace into" in OllyDbg
Example:
	ti

TO
--
Executes "Trace over" in OllyDbg
Example:
	to

VAR
---
Declare a variable to be used in the script. 
Must be done before the variable is used.
Example: 
	var x

XOR dest, src
-------------
XORs src and dest and stores result in dest
Example: 
	xor x, 0F
	xor eax, x
	xor [401000], 5


3.2 Labels
----------
Labels are defined bu using the label name followed by a colon.
Example:
	SOME_LABEL:


3.3 Comments
------------
Comments can be put anywhere and have to start with "//". Block
comments must start with "/*" on a new line and and with "*/"
also on a new line.


3.4 Menus
---------
The main OllyScript menu consists of the following items:
- Run script...: lets the user select a script file and starts it
- Abort: aborts a running script
- Pause: pauses a running script
- Resume: resumes a paused script
- About: shows information about this plugin


------------------------------

4. Contact me
-------------
To contact me you can post your question in the forum or go on IRC 
and message SHaG on EFnet. 

------------------------------

5. License
----------
Soon I'm going to armadildo this plugin and charge an awful lot of money
for it! :P Seriously, you are free to use this plugin and the source code however 
you see fit. However please name me in your documentation/about box and if 
the project you need my code for is on a larger scale please also notify 
me - I am curious.

------------------------------

6. Thanks!
----------
I'd like to thank:
- A. Focht and sgdt on OllyDbg users' board for helping me with many explanations and ideas.
- s0nkite for reporting bugs
- britedream, lownoise, FEUERRADER (privet =)) and R@dier for writing such nice scripts!
- And of course Olly, the man who wrote the magnificent debugger!

------------------------------