# Nordic Semiconductor Tutorial



# The [Nordic Semiconductor Infocenter](https://infocenter.nordicsemi.com) contains technical documentation for our current solutions and technologies.



# ![nRF51 Series](res/img/nRF51_Series.PNG)




# ![nRF52 Series](res/img/nRF52_Series.PNG)




# Dual-bank and single-bank updates

To safely perform a Device Firmware Update, the new firmware image should not be copied to the final location in memory until it has been validated. This ensures that only complete and valid images are activated. If an error occurs during the transfer, the firmware should not be updated.




## **Dual-bank updates**

During a dual-bank update, the existing bootloader, SoftDevice, or application is preserved until it is replaced by the new firmware image. The update process differs slightly depending on the type of image that is transferred.

### SoftDevice (with or without bootloader)
![nRF51 Series](res/img/dfu_bootloader_Dual_bank_updates1.svg)
DFU flash operations for SoftDevice and bootloader update

### Application or bootloader
![nRF51 Series](res/img/dfu_bootloader_Dual_bank_updates2.svg)
DFU flash operations for a dual-bank application update




## **Single-bank updates**

In a single-bank update, the existing application is replaced with the new application during the transfer of the image. Single-bank updates are available only for application updates, because if an error occurs and the device is left without a valid application, you can recover it by uploading a valid application again. If the device is left without a valid bootloader or SoftDevice, you can recover it only by attaching a flash tool and updating the device with a flash programmer.

The following figure shows the DFU process for an application in single-bank mode.
![nRF51 Series](res/img/dfu_bootloader_Single_bank_updates1.svg)
DFU flash operations for a single-bank application update

First, the existing application is erased to prepare for the DFU transfer. The transferred image is then stored at the location of the old application, thus between the current SoftDevice and bootloader. Existing application data can be retained; see Preserving application data for more information. When the transfer is completed, the bootloader will validate the new application. If it is valid, the bootloader will start it. If it is not valid, the bootloader will reset, start in DFU mode, and wait for a new image to be uploaded.
