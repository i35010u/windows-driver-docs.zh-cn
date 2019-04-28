---
title: EFI_USBFN_MESSAGE
description: EFI_USBFN_MESSAGE
ms.assetid: 411890e1-8913-4e47-acd5-1b36b1b05f34
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 339bed0bdd386b2c871f166bb6d62efa32891474
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337726"
---
# <a name="efiusbfnmessage"></a>EFI\_USBFN\_MESSAGE


**EFI\_USBFN\_消息**枚举用于指示启动了消息通知的事件

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
没有设备信息。

<a href="" id="efiusbmsgsetuppacket"></a>**EfiUsbMsgSetupPacket**  
指示接收安装数据包时，返回的缓冲区包含 EFI\_USB\_设备\_请求结构

<a href="" id="efiusbmsgendpointstatuschangedrx"></a>**EfiUsbMsgEndpointStatusChangedRx**  
指示所请求的数据的一些具有已收到来自主机。 它负责的类驱动程序来确定是否需要等待任何剩余数据。 返回的缓冲区包含 EFI\_USBFN\_传输\_结果结构包含终结点号、 传输状态和接收的字节数。

<a href="" id="efiusbmsgendpointstatuschangedtx"></a>**EfiUsbMsgEndpointStatusChangedTx**  
指示，某些请求的数据已经传输到主机。 它负责的类驱动程序来确定是否需要重新发送任何剩余数据。 返回的缓冲区包含 EFI\_USBFN\_传输\_结果结构包含终结点号、 transferstatus 和发送的字节数。

<a href="" id="efiusbmsgbuseventdetach"></a>**EfiUsbMsgBusEventDetach**  
分离总线事件发出信号。

<a href="" id="efiusbmsgbuseventattach"></a>**EfiUsbMsgBusEventAttach**  
附加总线事件发出信号。

<a href="" id="efiusbmsgbuseventreset"></a>**EfiUsbMsgBusEventReset**  
重置总线事件发出信号。

<a href="" id="efiusbmsgbuseventsuspend"></a>**EfiUsbMsgBusEventSuspend**  
挂起总线事件发出信号。

<a href="" id="efiusbmsgbuseventresume"></a>**EfiUsbMsgBusEventResume**  
恢复总线事件发出信号。

<a href="" id="efiusbmsgbuseventspeed"></a>**EfiUsbMsgBusEventSpeed**  
总线速度更新，总线速度使用指示返回的缓冲区[EFI\_USB\_总线\_速度](efi-usb-bus-speed.md)枚举。

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




