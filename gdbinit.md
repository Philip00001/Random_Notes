\# (this line is optional) set auto-load safe-path $(pwd)
 

set logging enabled on

file /Users/tl_l/my-app/target/thumbv7m-none-eabi/debug/hello

target extended-remote :3333

set print asm-demangle on

break DefaultHandler

break HardFault

monitor arm semihosting enable

load

break main

continue