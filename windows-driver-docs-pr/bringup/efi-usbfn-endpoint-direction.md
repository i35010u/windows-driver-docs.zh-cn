---
title: EFI_USBFN_ENDPOINT_DIRECTION
description: EFI_USBFN_ENDPOINT_DIRECTION
ms.assetid: 910f7ab5-b4c0-4385-9306-37d863d19bf7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f45aef9754542f8242294e1fcb2229478cd0d05c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337782"
---
# <a name="efiusbfnendpointdirection"></a>EFI\_USBFN\_ENDPOINT\_DIRECTION


**EFI\_USBFN\_终结点\_方向**枚举用于标识 USB 传输的方向。

## <a name="syntax"></a>语法


```cpp
typedef enum _EFI_USBFN_ENDPOINT_DIRECTION 
{
    EfiUsbEndpointDirectionHostOut  = 0,
    EfiUsbEndpointDirectionHostIn,
    EfiUsbEndpointDirectionDeviceTx = EfiUsbEndpointDirectionHostIn,
    EfiUsbEndpointDirectionDeviceRx = EfiUsbEndpointDirectionHostOut
} EFI_USBFN_ENDPOINT_DIRECTION;
```

## <a name="constants"></a>常量


<a href="" id="efiusbendpointdirectionhostout"></a>**EfiUsbEndpointDirectionHostOut**  
指示出 USB 传输。 D irection 是从主机到设备

<a href="" id="efiusbendpointdirectionhostin"></a>**EfiUsbEndpointDirectionHostIn**  
指示 USB 中传输。 方向是从设备到主机。

<a href="" id="efiusbendpointdirectiondevicetx"></a>**EfiUsbEndpointDirectionDeviceTx**  
指示 USB 中传输。 方向是从设备到主机。

<a href="" id="efiusbendpointdirectiondevicerx"></a>**EfiUsbEndpointDirectionDeviceRx**  
指示出 USB 传输。 方向是从主机到设备

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




