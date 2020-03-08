First install nasm by running `sudo apt-get install nasm` in your linux terminal.<br>
Write the below assembly code and rename the file as `shell.asm` <br>

    section .data
      msg db '/bin/sh'
      
    section .text
      global _start
      
    _start:
      mov eax, 11
      mov ebx, msg
      mov ecx, 0
      int 0x80
      
      mov eax, 1
      mov ebx, 0
      int 0x80
      
save the .asm file<br><br>
When compiling, if we use <br>
`nasm -f elf -o shell.o shell.asm`  and <br>
`ld -o shell shell.o` <br><br>
In my case it will get an error because the assembly code is written in x86 architecture.<br>
![](https://user-images.githubusercontent.com/37071700/76168122-82744980-6192-11ea-8cee-21a50debc49d.PNG) <br><br>
To address this issue we can use, <br>`nasm -f elf64 -o shell.o shell.asm` and <br>`ld -m elf_x86_64 -s -o shell shell.o`<br> as the compiling commands. And then we can use `./shell` to spawn a shell.<br>
![](https://user-images.githubusercontent.com/37071700/76168126-8738fd80-6192-11ea-94bf-7c15a2d9da58.PNG)<br><br>
