Blinky example for the stm32f401 "blackpill" devkit.

# UDEV rules

You can use a group that your user belogs to, like uucp/dialout:

    # STMicroelectronics STM32F4x
    ATTRS{idVendor}=="0483", ATTRS{idProduct}=="5740", GROUP:="uucp"

    # STMicroelectronics device in DFU mode
    ATTRS{idVendor}=="0483", ATTRS{idProduct}=="df11", GROUP:="uucp"

Or allow read-write to every user:

    # STMicroelectronics STM32F4x
    ATTRS{idVendor}=="0483", ATTRS{idProduct}=="5740", MODE:="0666"

    # STMicroelectronics device in DFU mode
    ATTRS{idVendor}=="0483", ATTRS{idProduct}=="df11", MODE:="0666"

# Tools and dependencies

    rustup component add llvm-tools-preview
    rustup target add thumbv7em-none-eabihf
    cargo install cargo-make cargo-binutils itm
    pacman -S dfu-util openocd arm-none-eabi-gdb

# Flash with USB bootloader

Reset the device while keeping the BOOT0 button pressed, then use `cargo make dfu` to flash the firmware.

# Flash with openocf

    cargo run flash
