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
