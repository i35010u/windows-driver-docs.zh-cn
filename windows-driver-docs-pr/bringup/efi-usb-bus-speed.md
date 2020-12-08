---
title: EFI_USB_BUS_SPEED
description: EFI_USB_BUS_SPEED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 492a432837146de0ab183beb6995297edd337793
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803393"
---
# <a name="efi_usb_bus_speed"></a>EFI \_ USB \_ 总线 \_ 速度


Is 枚举包含用于指示总线速度的值。

## <a name="syntax"></a>语法


```cpp
typedef enum _EFI_USB_BUS_SPEED 
{
    UsbBusSpeedUnknown = 0,
    UsbBusSpeedLow,
    UsbBusSpeedFull,
    UsbBusSpeedHigh,
    UsbBusSpeedSuper,
    UsbBusSpeedMaximum = UsbBusSpeedSuper
} EFI_USB_BUS_SPEED;
```

## <a name="constants"></a>常量


<a href="" id="usbbusspeedunknown"></a>**UsbBusSpeedUnknown**  
总线速度未知。

<a href="" id="usbbusspeedlow"></a>**UsbBusSpeedLow**  
低速。

<a href="" id="usbbusspeedfull"></a>**UsbBusSpeedFull**  
全速。

<a href="" id="usbbusspeedhigh"></a>**UsbBusSpeedHigh**  
高速。

<a href="" id="usbbusspeedsuper"></a>**UsbBusSpeedSuper**  
速度非常快。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




