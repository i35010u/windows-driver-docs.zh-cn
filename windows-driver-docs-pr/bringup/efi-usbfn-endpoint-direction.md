---
title: EFI_USBFN_ENDPOINT_DIRECTION
description: EFI_USBFN_ENDPOINT_DIRECTION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79b17e357fc5efe88ca43dcf964f28a9c851721e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789051"
---
# <a name="efi_usbfn_endpoint_direction"></a>EFI \_ USBFN \_ 终结点 \_ 方向


**EFI \_ USBFN \_ 终结点 \_ 方向** 枚举用于标识 USB 传输方向。

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
指示 USB 传出传输。 D irection 是从主机到设备的

<a href="" id="efiusbendpointdirectionhostin"></a>**EfiUsbEndpointDirectionHostIn**  
指示传输中有 USB。 方向是从设备到主机。

<a href="" id="efiusbendpointdirectiondevicetx"></a>**EfiUsbEndpointDirectionDeviceTx**  
指示传输中有 USB。 方向是从设备到主机。

<a href="" id="efiusbendpointdirectiondevicerx"></a>**EfiUsbEndpointDirectionDeviceRx**  
指示 USB 传出传输。 方向是从主机到设备

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




