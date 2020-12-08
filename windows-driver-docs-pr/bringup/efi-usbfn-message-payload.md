---
title: EFI_USBFN_MESSAGE_PAYLOAD
description: EFI_USBFN_MESSAGE_PAYLOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91981c0ba6cb36baaf2b0af56286adc430eccdbf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803359"
---
# <a name="efi_usbfn_message_payload"></a>EFI \_ USBFN \_ 消息 \_ 有效负载


**EFI \_ USBFN \_ 消息 \_ 负载** 联合包含当前消息) 的其他负载 (设备请求、传输结果或总线速度信息。

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
一个 **EFI \_ USB \_ 设备 \_ 请求** 结构，其中包含有关设备请求的信息。

<a href="" id="utr"></a>**utr**  
一个 [EFI \_ USBFN \_ 传输 \_ 结果](efi-usbfn-transfer-result.md) 结构，其中包含有关传输结果的信息。

<a href="" id="ubs"></a>**ubs**  
用于指示 USB 总线速度的 [EFI \_ usb \_ 总线 \_ 速度](efi-usb-bus-speed.md) 枚举值。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




