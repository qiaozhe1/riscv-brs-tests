# RISC-V Boot and Runtime Services Test Suite.

For more information on The Boot and Runtime Services(BRS) please see：[RISC-V Boot and Runtime Services (BRS) Specification](https://github.com/riscv-non-isa/riscv-brs).

This project is rebuilt based on [rv-brs-test-suite](https://github.com/intel/rv-brs-test-suite) to simplify the brs-tests test environment construction process. Currently includes [edk2-test](https://github.com/tianocore/edk2-test) and [SBI-test](https://gitlab.com/jones-drew/kvm-unit-tests.git).

To prevent potential issues, build on ubuntu22.04 and have enough disk space on the system. At the same time, make sure that the following software is installed：curl mtools gdisk gcc openssl automake autotools-dev libtool bison flex bc uuid-dev python3 libglib2.0-dev libssl-dev autopoint gcc-riscv64-unknown-elf gcc g++

## Construct

```
git clone https://github.com/riscv-software-src/riscv-brs-tests.git

cd riscv-brs-tests && ./build.sh
```

The build.sh script will execute the Makefiles in each directory under /src one by one and build the image. The sources of these components are as follows：

| project   | source                                            | tag/branch                               |
| --------- | ------------------------------------------------- | ---------------------------------------- |
| buildroot | https://github.com/buildroot/buildroot.git        | 2023.11                                  |
| edk2-test | https://github.com/tianocore/edk2-test.git        | 81dfa8d53d4290366ae41e1f4c2ed6d6c5016c07 |
| edk2      | https://github.com/tianocore/edk2.git             | edk2-stable202308                        |
| grub      | https://git.savannah.gnu.org/git/grub.git         | grub-2.12                                |
| linux     | https://github.com/vlsunil/linux.git              | acpi_b2_v2_riscv_aia_v11                 |
| opensbi   | https://github.com/riscv-software-src/opensbi.git | v1.3.1                                   |
| qemu      | https://github.com/vlsunil/qemu.git               | riscv_acpi_b2_v7                         |
| SBI-test  | https://gitlab.com/jones-drew/kvm-unit-tests.git  | riscv/x-tests                            |

The built image is located at /target/brs_live_image.img.

```
./target/start_uefi_sct.sh
```
This script starts qemu and automatically performs edk2-test and sbi-test tests.

## License
Licensed under the Apache License v2.0.
