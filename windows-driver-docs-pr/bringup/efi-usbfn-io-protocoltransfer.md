---
title: EFI_USBFN_IO_PROTOCOL.Transfer
description: EFI_USBFN_IO_PROTOCOL.Transfer
ms.assetid: 0585de75-9268-4964-8c5f-dcc3338e5287
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08f45877b8a785f11f09f6672e3a349e4489b323
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337675"
---
# <a name="efiusbfnioprotocoltransfer"></a>EFI\_USBFN\_IO\_PROTOCOL.Transfer


**传输**函数上指定的终结点相互传输数据从主机的句柄。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Direction</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EfiUsbEndpointDirectionDeviceTx</p></td>
<td><p>在指定的终结点上启动传输传输并立即返回。</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbEndpointDirectionDeviceRx</p></td>
<td><p>指定的终结点上启动接收传输并立即返回可用数据。</p></td>
</tr>
</tbody>
</table>

 

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI *EFI_USBFN_IO_TRANSFER) (
  IN EFI_USBFN_IO_PROTOCOL         *This,
  IN UINT8                         EndpointIndex,
  IN EFI_USBFN_ENDPOINT_DIRECTION  Direction,
  IN OUT UINTN                     *BufferSize,
  IN OUT VOID                      *Buffer
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="endpointindex"></a>*EndpointIndex*  
指示终结点的 TX 或 RX 传输需要执行的。

<a href="" id="direction"></a>*方向*  
终结点的方向。 有关详细信息，请参阅[EFI\_USBFN\_终结点\_方向](efi-usbfn-endpoint-direction.md)。

<a href="" id="buffersize"></a>*BufferSize*  
如果方向是**EfiUsbEndpointDirectionDeviceRx**:在输入，以字节为单位的缓冲区的大小。 在输出时，以字节为单位的缓冲区中返回数据量。 如果方向是**EfiUsbEndpointDirectionDeviceTx**:在输入，以字节为单位的缓冲区的大小。 在输出时，实际上以字节为单位传输的数据量。

<a href="" id="buffer"></a>*缓冲区*  
如果方向是**EfiUsbEndpointDirectionDeviceRx**： 要返回接收到的数据的缓冲区。

如果方向是**EfiUsbEndpointDirectionDeviceTx**:包含要传输的数据的缓冲区。

**请注意**  分配和使用的 AllocateTransferBuffer 和 FreeTransferBuffer 函数释放此缓冲区。 此函数的调用方不能释放或重复使用之前的缓冲区**EfiUsbMsgEndpointStatusChangedRx**或**EfiUsbMsgEndpointStatusChangedTx**的地址以及收到消息作为消息负载的一部分的传输缓冲区。 请参阅[EFI\_USBFN\_IO\_协议。事件处理程序](efi-usbfn-io-protocoleventhandler.md)的各种消息和及其有效负载的详细信息。

 

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
</tbody>
</table>

 

## <a name="remarks"></a>备注


类驱动程序必须调用[EFI\_USBFN\_IO\_协议。事件处理程序](efi-usbfn-io-protocoleventhandler.md)重复以接收更新的传输状态和不同的终结点上传输的字节数。 在传输状态更新时*缓冲区*字段[EFI\_USBFN\_传输\_结果](efi-usbfn-transfer-result.md)必须使用已缓冲区指针初始化结构提供给此方法。 此函数失败，出现 EFI\_无效\_参数返回代码，如果指定的方向不正确的终结点。

调用序列概述所示[UEFI 序列图](uefi-sequence-diagram.md)。

此函数失败，出现 EFI\_无效\_参数返回代码，如果指定的方向不正确的终结点。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




