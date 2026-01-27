https://github.com/stm32-rs/stm32f1xx-hal/blob/HEAD/.cargo/config.toml
https://crates.io/crates/stm32f1xx-hal
https://docs.rs/stm32f1xx-hal/latest/stm32f1xx_hal/

# Fixing Error
## package `stm32f1xx-hal` does have feature `rtic`
How to Fix: 
Replace your existing dependency entry with the following:
```toml
[dependencies]
# The 'rt' feature now resides in the 'stm32f1' PAC (Peripheral Access Crate) 
# which stm32f1xx-hal uses internally.
stm32f1xx-hal = { version = "0.11.0", features = ["stm32f103", "medium"] }
cortex-m-rt = "0.7"
```
# Pinout
![[stm32f103c6t6]]

# SPI
```rust
// This is NOT CORRECT
// TODO : FIX THIS 

let pins = (

gpioa.pa5.into_alternate_push_pull(&mut gpioa.crl), // SCK

gpioa.pa6.into_alternate_push_pull(&mut gpioa.crl), // MISO

gpioa.pa7.into_alternate_push_pull(&mut gpioa.crl), // MOSI

);
```

## SPI mode

## Overview of SPI Modes

The Serial Peripheral Interface (SPI) supports four different modes, which are defined by two parameters: Clock Polarity (CPOL) and Clock Phase (CPHA). These modes determine how data is transmitted and received between the master and slave devices.

## SPI Modes Table

| SPI MODE | CPOL | CPHA | DESCRIPTION                                                                                |
| -------- | ---- | ---- | ------------------------------------------------------------------------------------------ |
| 0        | 0    | 0    | Clock starts low; data is sampled on the rising edge and shifted out on the falling edge.  |
| 1        | 0    | 1    | Clock starts low; data is sampled on the falling edge and shifted out on the rising edge.  |
| 2        | 1    | 0    | Clock starts high; data is sampled on the rising edge and shifted out on the falling edge. |
| 3        | 1    | 1    | Clock starts high; data is sampled on the falling edge and shifted out on the rising edge. |

```
let mode = stm32f1xx_hal::spi::Mode {

polarity: stm32f1xx_hal::spi::Polarity::IdleLow, //CPOL = 0

phase: stm32f1xx_hal::spi::Phase::CaptureOnSecondTransition, //CPHA = 1 ?_?

};
```
# SPI Frequency

SPI frequency refers to the speed at which data is transmitted over the Serial Peripheral Interface, typically measured in Hertz (Hz). The maximum frequency can vary depending on the specific devices and configurations used, with some systems supporting frequencies up to 100 MHz or more.
# [[EPD_WAVESHARE]]

