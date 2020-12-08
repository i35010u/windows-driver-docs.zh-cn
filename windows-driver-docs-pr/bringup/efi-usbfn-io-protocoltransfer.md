---
title: EFI_USBFN_IO_PROTOCOL.Transfer
description: EFI_USBFN_IO_PROTOCOL.Transfer
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50b574428aebda6fb1ac0cbd76c97f3546467c9e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789027"
---
# <a name="efi_usbfn_io_protocoltransfer"></a>EFI \_ USBFN \_ IO \_ 协议。转换


**传输** 函数处理与指定终结点上的主机之间的数据传输。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方向</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EfiUsbEndpointDirectionDeviceTx</p></td>
<td><p>在指定终结点上启动传输传输并立即返回。</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbEndpointDirectionDeviceRx</p></td>
<td><p>在指定终结点上启动接收传输并立即返回可用数据。</p></td>
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

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

<a href="" id="endpointindex"></a>*EndpointIndex*  
指示需要进行 TX 或 RX 传输的终结点。

<a href="" id="direction"></a>*方向键*  
终结点的方向。 有关详细信息，请参阅 [EFI \_ USBFN \_ 终结点 \_ 方向](efi-usbfn-endpoint-direction.md)。

<a href="" id="buffersize"></a>*BufferSize*  
如果方向为 **EfiUsbEndpointDirectionDeviceRx**：输入，则缓冲区大小（以字节为单位）。 输出时，缓冲区中返回的数据量（以字节为单位）。 如果方向为 **EfiUsbEndpointDirectionDeviceTx**：输入，则缓冲区大小（以字节为单位）。 输出时，实际传输的数据量（以字节为单位）。

<a href="" id="buffer"></a>*宽限*  
如果方向为 **EfiUsbEndpointDirectionDeviceRx**：要返回接收数据的缓冲区。

如果方向为 **EfiUsbEndpointDirectionDeviceTx**：包含要传输的数据的缓冲区。

**注意**  
使用 AllocateTransferBuffer 和 FreeTransferBuffer 函数分配和释放此缓冲区。 此函数的调用方在接收 **EfiUsbMsgEndpointStatusChangedRx** 或 **EfiUsbMsgEndpointStatusChangedTx** 消息后，不能释放或重新使用缓冲区，直到收到作为消息负载一部分的传输缓冲区的地址。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。](efi-usbfn-io-protocoleventhandler.md) 有关各种消息及其有效负载的详细信息，请 EventHandler。

 

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
</tbody>
</table>

 

## <a name="remarks"></a>备注


类驱动程序必须调用 [EFI \_ USBFN \_ IO \_ 协议。重复 EventHandler](efi-usbfn-io-protocoleventhandler.md) 以接收有关传输状态的更新和在各种终结点上传输的字节数。 当更新传输状态时，必须用提供给此方法的缓冲区指针初始化 [EFI \_ USBFN \_ 传输 \_ 结果](efi-usbfn-transfer-result.md)结构的 *缓冲区* 字段。 如果指定的方向对于终结点不正确，则此函数将失败，并且 EFI \_ 无效 \_ 参数返回代码。

此调用序列的概述在 [UEFI 序列图](uefi-sequence-diagram.md)中进行了说明。

如果指定的方向对于终结点不正确，则此函数将失败，并且 EFI \_ 无效 \_ 参数返回代码。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




