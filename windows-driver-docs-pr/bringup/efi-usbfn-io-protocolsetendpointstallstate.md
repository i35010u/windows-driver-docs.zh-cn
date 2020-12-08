---
title: EFI_USBFN_IO_PROTOCOL.SetEndpointStallState
description: EFI_USBFN_IO_PROTOCOL.SetEndpointStallState
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd43534d24ca95d2b98c24d1889584a252648efd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803363"
---
# <a name="efi_usbfn_io_protocolsetendpointstallstate"></a>EFI \_ USBFN \_ IO \_ 协议。SetEndpointStallState


**SetEndpointStallState** 函数设置或清除指定终结点上的延迟状态。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_SET_ENDPOINT_STALL_STATE) (
  IN EFI_USBFN_IO_PROTOCOL        *This,
  IN UINT8                        EndpointIndex,
  IN EFI_USBFN_ENDPOINT_DIRECTION Direction,
  IN BOOLEAN                      State
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

<a href="" id="endpointindex"></a>*EndpointIndex*  
指示需要停止的终结点。

<a href="" id="direction"></a>*方向键*  
终结点的方向。 有关详细信息，请参阅 [EFI \_ USBFN \_ 终结点 \_ 方向](efi-usbfn-endpoint-direction.md)。

<a href="" id="state"></a>*状态*  
指定终结点上请求的挂起状态。 如果将此参数设置为 **TRUE** ，则终结点将会卡住。 如果将其设置为 **FALSE** ，则会清除现有的延迟。

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


如果指定的方向对于终结点不正确，则此函数将失败，并且 **EFI \_ 无效 \_ 参数** 。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




