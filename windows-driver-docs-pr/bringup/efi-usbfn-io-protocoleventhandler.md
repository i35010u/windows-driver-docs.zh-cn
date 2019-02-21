---
title: EFI_USBFN_IO_PROTOCOL.EventHandler
description: EFI_USBFN_IO_PROTOCOL.EventHandler
ms.assetid: d493de90-cb8c-44d1-8999-f1ceb26e5c15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff785fedb41a40e0425fbb75465aec14a94368c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547731"
---
# <a name="efiusbfnioprotocoleventhandler"></a>EFI\_USBFN\_IO\_PROTOCOL.EventHandler


**EventHandler**函数重复调用，以接收有关 USB 总线状态更新、 接收和传输上的终结点的状态更改并设置终结点 0 上的数据包。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_EVENTHANDLER) (
  IN EFI_USBFN_IO_PROTOCOL        *This,
  OUT EFI_USBFN_MESSAGE           *Message,
  IN OUT UINTN                    *PayloadSize,
  OUT EFI_USBFN_MESSAGE_PAYLOAD   *Payload
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="message"></a>*消息*  
一个[EFI\_USBFN\_消息](efi-usbfn-message.md)值，该值指示启动此通知的事件。

<a href="" id="payloadsize"></a>*PayloadSize*  
在输入时，内存的大小指向的有效负载。 在输出时，负载中返回数据量。

<a href="" id="payload"></a>*有效负载*  
一个指向[EFI\_USBFN\_消息\_负载](efi-usbfn-message-payload.md)实例中要返回当前消息的额外负载。

## <a name="return-values"></a>返回值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EFI_SUCCESS</strong></p></td>
<td><p>成功返回的函数</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>参数无效</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理设备报告了错误。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_NOT_READY</strong></p></td>
<td><p>物理设备是正忙还是未准备好处理此请求</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_BUFFER_TOO_SMALL</strong></p></td>
<td><p>提供的缓冲区不足够大以保存消息负载。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


类驱动程序必须调用事件处理程序重复以接收更新的传输状态和不同的终结点上传输的字节数。 请参阅[UEFI 序列图](uefi-sequence-diagram.md)有关进一步信息。

一些消息具有关联有效负载中提供的缓冲区返回的。 下表介绍各种消息和及其有效负载。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>消息</th>
<th>有效负载</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EfiUsbMsgSetupPacket</p></td>
<td><p>EFI_USB_DEVICE_REQUEST</p></td>
<td><p>接收安装数据包</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbMsgEndpointStatusChangedRx</p></td>
<td><p><a href="efi-usbfn-transfer-result.md" data-raw-source="[EFI_USBFN_TRANSFER_RESULT](efi-usbfn-transfer-result.md)">EFI_USBFN_TRANSFER_RESULT</a></p></td>
<td><p>某些请求的数据已传输到主机。 它负责的类驱动程序来确定是否需要重新发送任何剩余数据。 缓冲区提供给<a href="efi-usbfn-io-protocoltransfer.md" data-raw-source="[EFI_USBFN_IO_PROTOCOL.Transfer](efi-usbfn-io-protocoltransfer.md)">EFI_USBFN_IO_PROTOCOL。传输</a>r 必须与有效负载的缓冲区字段相同。</p></td>
</tr>
<tr class="odd">
<td><p>EfiUsbMsgEndpointStatusChangedTx</p></td>
<td><p><a href="efi-usbfn-transfer-result.md" data-raw-source="[EFI_USBFN_TRANSFER_RESULT](efi-usbfn-transfer-result.md)">EFI_USBFN_TRANSFER_RESULT</a></p></td>
<td><p>已从主机收到一些请求的数据。 它负责的类驱动程序来确定是否需要等待任何剩余数据。 缓冲区提供给<a href="efi-usbfn-io-protocoltransfer.md" data-raw-source="[EFI_USBFN_IO_PROTOCOL.Transfer](efi-usbfn-io-protocoltransfer.md)">EFI_USBFN_IO_PROTOCOL。传输</a>必须与有效负载的缓冲区字段相同。</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbMsgBusEventReset</p></td>
<td><p>无</p></td>
<td><p>重置总线事件收到信号。</p></td>
</tr>
<tr class="odd">
<td><p>EfiUsbMsgBusEventDetach</p></td>
<td><p>无</p></td>
<td><p>分离总线事件收到信号。</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbMsgBusEventAttach</p></td>
<td><p>无</p></td>
<td><p>附加总线事件发出信号。</p></td>
</tr>
<tr class="odd">
<td><p>EfiUsbMsgBusEventSuspend</p></td>
<td><p>无</p></td>
<td><p>挂起总线事件收到信号。</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbMsgBusEventResume</p></td>
<td><p>无</p></td>
<td><p>恢复总线事件发出信号。</p></td>
</tr>
<tr class="odd">
<td><p>EfiUsbMsgBusEventSpeed</p></td>
<td><p><a href="efi-usb-bus-speed.md" data-raw-source="[EFI_USB_BUS_SPEED](efi-usb-bus-speed.md)">EFI_USB_BUS_SPEED</a></p></td>
<td><p>总线速度更新用信号通知。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




