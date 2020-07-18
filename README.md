# android_udoo_manifest
    
## u-boot for Android
* Booting Android with u-boot : u-boot-2020.07/doc/android/boot-image.rst    
* IMX partitioning info for android bootup : Android_User's_Guide.pdf    
* Other reference board : https://www.nxp.com/document/guide/getting-started-with-i-mx-6-solox-sabre:GS-RD-IMX6SX-SABRE#title1.2    
* Udoo doc : https://www.udoo.org/docs-neo/Advanced_Topics/Compile_Android_From_Source.html    
* Partitioning info at source.android.com : https://source.android.com/devices/architecture/dto/partitions
    
## TODO
* integrate fsl_gpu.mk
* all fsl related .so from https://github.com/UDOOboard/android_device_fsl-proprietary/tree/android-6.0.1/gpu-viv
* TARGET_KERNEL_MODULES in BoardConfigs.mk
* BOARD_SEPOLICY_DIRS in BoardConfigs.mk
* Add release build key for platform app signing, build/target/product/security/README contains more detail. Put something like for device/udoo/common/security. Not required for development build.
* To enable kernel compilation or to include precompiled. At present TARGET_NO_KERNEL := true in BoardConfigs.mk to ignore kernel for time being.
* To enable bootloader compilation or to include precompiled. At present TARGET_NO_BOOTLOADER := true in BoardConfigs.mk to ignore bootloader for time being.

## Compiling u-boot with android support
    
``
make distclean && make udoo_neo_defconfig CONFIG_CMD_BOOT_ANDROID=y CONFIG_ANDROID_BOOT_IMAGE=y CONFIG_CMD_LOAD_ANDROID=y CONFIG_ANDROID_BOOTLOADER=y all -j8
``
## BoardConfig.mk for Android 10
    
```
ARGET_NO_KERNEL := false
BOARD_KERNEL_CMDLINE := console=ttymxc0,115200 init=/init vmalloc=256M androidboot.console=ttymxc0 consoleblank=0 androidboot.hardware=freescale cma=128M androidboot.selinux=disabled androidboot.dm_verity=disabled no_console_suspend
BOARD_KERNEL_CMDLINE += uart_from_osc clk_ignore_unused

PRODUCT_COPY_FILES += device/udoo/udooneo_6sx-kernel/zImage:kernel
BOARD_INCLUDE_DTB_IN_BOOTIMG := true
BOARD_PREBUILT_DTBIMAGE_DIR := device/udoo/udooneo_6sx-kernel/dts

TARGET_UBOOT_VERSION := uboot-imx
TARGET_BOOTLOADER_CONFIG := imx6sx:udoo_neo_android_defconfig
TARGET_KERNEL_DEFCONF := udoo_neo_android_defconfig
BOARD_BOOTIMG_HEADER_VERSION := 2
BOARD_MKBOOTIMG_ARGS := --header_version $(BOARD_BOOTIMG_HEADER_VERSION)
```
