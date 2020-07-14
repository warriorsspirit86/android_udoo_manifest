# android_udoo_manifest

## TODO
* integrate fsl_gpu.mk
* all fsl related .so from https://github.com/UDOOboard/android_device_fsl-proprietary/tree/android-6.0.1/gpu-viv
* TARGET_KERNEL_MODULES in BoardConfigs.mk
* BOARD_SEPOLICY_DIRS in BoardConfigs.mk
* Add release build key for platform app signing, build/target/product/security/README contains more detail. Put something like for device/udoo/common/security. Not required for development build.
* To enable kernel compilation or to include precompiled. At present TARGET_NO_KERNEL := true in BoardConfigs.mk to ignore kernel for time being.
* To enable bootloader compilation or to include precompiled. At present TARGET_NO_BOOTLOADER := true in BoardConfigs.mk to ignore bootloader for time being.
