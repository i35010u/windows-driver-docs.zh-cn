---
title: EFI_USBFN_MESSAGE_PAYLOAD
description: EFI_USBFN_MESSAGE_PAYLOAD
ms.assetid: 88d32ce1-460d-4c0f-b42a-426f42e2f969
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00b32ff2827250cde4e627c71982a5eb3fdae81d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337707"
---
# <a name="efiusbfnmessagepayload"></a>EFI\_USBFN\_消息\_有效负载


**EFI\_USBFN\_消息\_负载**联合包含当前消息的额外负载 （设备请求、 传输结果或总线速度信息）。

## <a name="syntax"></a>语法


```cpp
typedef union _EFI_USBFN_MESSAGE_PAYLOAD
{
    EFI_USB_DEVICE_REQUEST      udr;
    EFI_USBFN_TRANSFER_RESULT   utr;
    EFI_USB_BUS_SPEED           ubs;
} EFI_USBFN_MESSAGE_PAYLOAD;
```

## <a name="members"></a>成员


<a href="" id="udr"></a>**udr**  
一个**EFI\_USB\_设备\_请求**结构，其中包含有关设备请求的信息。

<a href="" id="utr"></a>**utr**  
一个[EFI\_USBFN\_传输\_结果](efi-usbfn-transfer-result.md)结构，其中包含有关传输结果的信息。

<a href="" id="ubs"></a>**ubs**  
一个[EFI\_USB\_总线\_速度](efi-usb-bus-speed.md)枚举值，该值指示 USB 总线速度。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




