---
title: EFI_USBFN_IO_PROTOCOL.EventHandler
description: EFI_USBFN_IO_PROTOCOL.EventHandler
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f84a6bfc9c551b028b2f93fc54ce096f5609b6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789031"
---
# <a name="efi_usbfn_io_protocoleventhandler"></a>EFI \_ USBFN \_ IO \_ 协议。EventHandler


重复调用 **EventHandler** 函数，接收有关 USB 总线状态的更新，接收和传输终结点上的状态更改，并在终结点0上设置数据包。

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
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

<a href="" id="message"></a>*消息*  
一个 [EFI \_ USBFN \_ 消息](efi-usbfn-message.md) 值，该值指示启动此通知的事件。

<a href="" id="payloadsize"></a>*PayloadSize*  
输入时，负载所指向的内存的大小。 输出时，负载中返回的数据量。

<a href="" id="payload"></a>*负载*  
一个指针，指向 [EFI \_ USBFN \_ 消息 \_ 负载](efi-usbfn-message-payload.md) 实例以返回当前消息的其他有效负载。

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
<td><p>函数已成功返回</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>参数无效</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理设备报告了一个错误。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_NOT_READY</strong></p></td>
<td><p>物理设备处于繁忙状态或尚未准备好处理此请求</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_BUFFER_TOO_SMALL</strong></p></td>
<td><p>提供的缓冲区不够大，无法容纳消息有效负载。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


类驱动程序必须重复调用 EventHandler，以接收有关传输状态的更新和在各种终结点上传输的字节数。 有关详细信息，请参阅 [UEFI 序列图](uefi-sequence-diagram.md) 。

一些消息具有在提供的缓冲区中返回的关联负载。 下表描述了各种消息及其有效负载。

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
<td><p>已收到安装数据包</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbMsgEndpointStatusChangedRx</p></td>
<td><p><a href="efi-usbfn-transfer-result.md" data-raw-source="[EFI_USBFN_TRANSFER_RESULT](efi-usbfn-transfer-result.md)">EFI_USBFN_TRANSFER_RESULT</a></p></td>
<td><p>某些请求的数据已传输到主机。 类驱动程序负责确定是否需要重新发送剩余的数据。 提供给 EFI_USBFN_IO_PROTOCOL 的缓冲区 <a href="efi-usbfn-io-protocoltransfer.md" data-raw-source="[EFI_USBFN_IO_PROTOCOL.Transfer](efi-usbfn-io-protocoltransfer.md)">。传输</a>r 必须与有效负载的 "缓冲区" 字段相同。</p></td>
</tr>
<tr class="odd">
<td><p>EfiUsbMsgEndpointStatusChangedTx</p></td>
<td><p><a href="efi-usbfn-transfer-result.md" data-raw-source="[EFI_USBFN_TRANSFER_RESULT](efi-usbfn-transfer-result.md)">EFI_USBFN_TRANSFER_RESULT</a></p></td>
<td><p>已从主机接收到一些请求的数据。 类驱动程序负责确定是否需要等待剩余的数据。 提供给 EFI_USBFN_IO_PROTOCOL 的缓冲区 <a href="efi-usbfn-io-protocoltransfer.md" data-raw-source="[EFI_USBFN_IO_PROTOCOL.Transfer](efi-usbfn-io-protocoltransfer.md)">。传输</a> 必须与有效负载的缓冲区字段相同。</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbMsgBusEventReset</p></td>
<td><p>无</p></td>
<td><p>重置总线事件已发出信号。</p></td>
</tr>
<tr class="odd">
<td><p>EfiUsbMsgBusEventDetach</p></td>
<td><p>无</p></td>
<td><p>已向分离总线事件发出信号。</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbMsgBusEventAttach</p></td>
<td><p>无</p></td>
<td><p>附加总线事件信号。</p></td>
</tr>
<tr class="odd">
<td><p>EfiUsbMsgBusEventSuspend</p></td>
<td><p>无</p></td>
<td><p>暂停总线事件已发出信号。</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbMsgBusEventResume</p></td>
<td><p>无</p></td>
<td><p>继续向总线事件发出信号。</p></td>
</tr>
<tr class="odd">
<td><p>EfiUsbMsgBusEventSpeed</p></td>
<td><p><a href="efi-usb-bus-speed.md" data-raw-source="[EFI_USB_BUS_SPEED](efi-usb-bus-speed.md)">EFI_USB_BUS_SPEED</a></p></td>
<td><p>总线速度更新已终止。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




