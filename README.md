#### Tutorial by Shival
## Bootloader

<a href="https://www.canva.com/design/DAFYvYbNOak/Hn6Yqwb8OLaUepgR8-kjwA/view">Presentation on bootloader</a><br/>
<a href="https://shival-gupta.github.io/bootloader/">Webpage documentation</a><br/>
<a href="https://drive.google.com/file/d/1YraA1utTeyUMTjPg5oDsDc9CtU5oCol_/view?usp=share_link">Bootloader manual</a><br/>
<hr/>

**Install NASM**

<A HREF="https://www.nasm.us/pub/nasm/releasebuilds/2.16.01/nasm-2.16.01.tar.gz"><b>Direct Download link: NASM</b></A><br/>
<A HREF="https://www.nasm.us/pub/nasm/releasebuilds/2.16.01/"><b>Browse NASM Release Builds</b></A><br/>

```
./configure
make
make install
whereis nasm
```

- **firstBootloader.asm**
```
[BITS 16]
[ORG 0x7C00]
JMP $
TIMES 510 - ($ - $$) db 0
DW 0xAA55
```

- **secondBootloader.asm**
```
[BITS 16]
[ORG 0x7C00]

MOV AL, 65
CALL PrintCharacter
JMP $

PrintCharacter:
MOV AH, 0x0E
MOV BH, 0x00
MOV BL, 0x07

INT 0x10
RET

TIMES 510 - ($ - $$) db 0
DW 0xAA55
```

- **thirdBootloader.asm**
```
[BITS 16]
[ORG 0x7C00]

MOV SI, HelloString
CALL PrintCharacter
JMP $

PrintCharacter:
MOV AH, 0x0E
MOV BH, 0x00
MOV BL, 0x07

INT 0x10
RET

PrintString:

next_character:
MOV AL, [SI]
INC SI
OR AL, AL
JZ exit_function
CALL PrintCharacter
JMP next_character
exit_function:
RET

HelloString db 'Hellow World', 0

TIMES 510 - ($ - $$) db 0
DW 0xAA55
```
