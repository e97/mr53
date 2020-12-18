# Meraki sources for MR53



`router-26-8-1-mr53-20201215.tar.bz2` contains OpenWRT + Linux kernel for MR53

`U-boot-MR53-20201215.tar.bz2` contains u-boot for MR53


## Build MR53 OpenWRT firmware:

Extract `router-26-8-1-mr53-20201215.tar.bz2`


```
cd meraki-firmware/openwrt
cp config-cryptid .config
make oldconfig
make -j1 BOARD=cryptid OPENWRT_EXTRA_BOARD_SUFFIX=_cryptid
```

## Build MR53 Linux-3.14 kernel:

Extract `router-26-8-1-mr53-20201215.tar.bz2`


```
cd meraki-firmware/linux-3.14
cp ../openwrt/target/linux/cryptid-3.14/config .config
make CROSS_COMPILE=../openwrt/staging_dir_arm_nofpu_cryptid/bin/arm-unknown-linux-uclibcgnueabi- ARCH=arm oldconfig
make CROSS_COMPILE=../openwrt/staging_dir_arm_nofpu_cryptid/bin/arm-unknown-linux-uclibcgnueabi- ARCH=arm prepare
touch rootlist
make CROSS_COMPILE=../openwrt/staging_dir_arm_nofpu_cryptid/bin/arm-unknown-linux-uclibcgnueabi- ARCH=arm vmlinux
```

## Build MR53 u-boot

Extract `U-boot-MR53-20201215.tar.bz2`

```
export CROSS_COMPILE=/path/to/arm32-cross-toolchain
cd U-boot.MR53
make sasquatch_config
make
```
