---
title: EFI_USBFN_DEVICE_INFO_ID
description: EFI_USBFN_DEVICE_INFO_ID
ms.assetid: bc0391b4-876a-4c3c-920c-a16a781a84b0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bbe90b7630b391c8c7a32d76b06518fc23dab10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337755"
---
# <a name="efiusbfndeviceinfoid"></a>EFI\_USBFN\_DEVICE\_INFO\_ID


此枚举用于标识对该驱动程序的请求中的特定字符串。

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
无效的 id。

<a href="" id="efiusbdeviceinfoserialnumber"></a>**EfiUsbDeviceInfoSerialNumber**  
对 USB 设备的序列号的请求。

<a href="" id="efiusbdeviceinfomanufacturername"></a>**EfiUsbDeviceInfoManufacturerName**  
制造商字符串的请求。

<a href="" id="efiusbdeviceinfoproductname"></a>**EfiUsbDeviceInfoProductName**  
对设备的产品名称的请求。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




