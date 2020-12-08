---
title: EFI_USBFN_MESSAGE
description: EFI_USBFN_MESSAGE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 194a414d4c4c994ea72e8931965bf59d0cf5811f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789009"
---
# <a name="efi_usbfn_message"></a>EFI \_ USBFN \_ 消息


**EFI \_ USBFN \_ 消息** 枚举用于指示启动消息通知的事件

## <a name="syntax"></a>语法


```cpp
typedef enum _EFI_USBFN_MESSAGE
{
EfiUsbMsgNone = 0,
EfiUsbMsgSetupPacket,
EfiUsbMsgEndpointStatusChangedRx,
EfiUsbMsgEndpointStatusChangedTx
EfiUsbMsgBusEventDetach,
EfiUsbMsgBusEventAttach,
EfiUsbMsgBusEventReset,
EfiUsbMsgBusEventSuspend,
EfiUsbMsgBusEventResume,
EfiUsbMsgBusEventSpeed
} EFI_USBFN_MESSAGE;
```

## <a name="constants"></a>常量


<a href="" id="efiusbmsgnone"></a>**EfiUsbMsgNone**  
无设备信息。

<a href="" id="efiusbmsgsetuppacket"></a>**EfiUsbMsgSetupPacket**  
指示收到安装数据包，返回的缓冲区包含 EFI \_ USB \_ 设备 \_ 请求结构

<a href="" id="efiusbmsgendpointstatuschangedrx"></a>**EfiUsbMsgEndpointStatusChangedRx**  
指示已从主机接收到一些请求的数据。 类驱动程序负责确定是否需要等待剩余的数据。 返回的缓冲区包含一个 EFI \_ USBFN \_ 传输 \_ 结果结构，其中包含终结点号、传输状态和接收的字节数。

<a href="" id="efiusbmsgendpointstatuschangedtx"></a>**EfiUsbMsgEndpointStatusChangedTx**  
指示某些请求的数据已传输到主机。 类驱动程序负责确定是否需要重新发送剩余的数据。 返回的缓冲区包含一个 EFI \_ USBFN \_ 传输 \_ 结果结构，其中包含终结点号、transferstatus 和发送的字节数。

<a href="" id="efiusbmsgbuseventdetach"></a>**EfiUsbMsgBusEventDetach**  
分离总线事件已发出信号。

<a href="" id="efiusbmsgbuseventattach"></a>**EfiUsbMsgBusEventAttach**  
附加总线事件信号。

<a href="" id="efiusbmsgbuseventreset"></a>**EfiUsbMsgBusEventReset**  
重置总线事件的信号。

<a href="" id="efiusbmsgbuseventsuspend"></a>**EfiUsbMsgBusEventSuspend**  
暂停总线事件的信号。

<a href="" id="efiusbmsgbuseventresume"></a>**EfiUsbMsgBusEventResume**  
继续向总线事件发出信号。

<a href="" id="efiusbmsgbuseventspeed"></a>**EfiUsbMsgBusEventSpeed**  
总线速度已更新，返回的缓冲区使用 [EFI \_ USB \_ 总线 \_ 速度](efi-usb-bus-speed.md) 枚举指示总线速度。

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




