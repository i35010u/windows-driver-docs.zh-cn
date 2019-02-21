---
title: EFI_USB_BUS_SPEED
description: EFI_USB_BUS_SPEED
ms.assetid: 2888cff6-db12-47ea-866f-de218e2b08e5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 179b6a0befdecc81e05d2fae07352396251f1d3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546430"
---
# <a name="efiusbbusspeed"></a>EFI\_USB\_BUS\_SPEED


枚举包含用来指示总线速度的值。

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
未知的总线速度。

<a href="" id="usbbusspeedlow"></a>**UsbBusSpeedLow**  
低速度。

<a href="" id="usbbusspeedfull"></a>**UsbBusSpeedFull**  
完整的速度。

<a href="" id="usbbusspeedhigh"></a>**UsbBusSpeedHigh**  
高速度。

<a href="" id="usbbusspeedsuper"></a>**UsbBusSpeedSuper**  
超级速度。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




