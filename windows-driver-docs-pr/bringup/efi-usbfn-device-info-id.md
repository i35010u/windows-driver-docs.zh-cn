---
title: EFI_USBFN_DEVICE_INFO_ID
description: EFI_USBFN_DEVICE_INFO_ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 771e1c6ac556f35bc378c20bb233cb69e851c3df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803383"
---
# <a name="efi_usbfn_device_info_id"></a>EFI \_ USBFN \_ 设备 \_ 信息 \_ ID


此枚举用于标识对驱动程序的请求中的特定字符串。

## <a name="syntax"></a>语法


```cpp
typedef enum _EFI_USBFN_DEVICE_INFO_ID   
{
    EfiUsbDeviceInfoUnknown = 0,
    EfiUsbDeviceInfoSerialNumber,
    EfiUsbDeviceInfoManufacturerName,
    EfiUsbDeviceInfoProductName
} EFI_USBFN_DEVICE_INFO_ID;
```

## <a name="constants"></a>常量


<a href="" id="efiusbdeviceinfounknown"></a>**EfiUsbDeviceInfoUnknown**  
ID 无效。

<a href="" id="efiusbdeviceinfoserialnumber"></a>**EfiUsbDeviceInfoSerialNumber**  
对 USB 设备序列号的请求。

<a href="" id="efiusbdeviceinfomanufacturername"></a>**EfiUsbDeviceInfoManufacturerName**  
对制造商字符串的请求。

<a href="" id="efiusbdeviceinfoproductname"></a>**EfiUsbDeviceInfoProductName**  
对设备产品名称的请求。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




