---
title: EFI_USBFN_IO_PROTOCOL.GetEndpointStallState
description: EFI_USBFN_IO_PROTOCOL.GetEndpointStallState
ms.assetid: abf53ee7-8460-4861-a82d-827ad1dc6c40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6fde5a4b46ca52fb6f41725974508377ab830d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564892"
---
# <a name="efiusbfnioprotocolgetendpointstallstate"></a>EFI\_USBFN\_IO\_PROTOCOL.GetEndpointStallState


**GetEndpointStallState**函数返回指定终结点上停止状态。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_GET_ENDPOINT_STALL_STATE) (
  IN EFI_USBFN_IO_PROTOCOL        *This,
  IN UINT8                        EndpointIndex,
  IN EFI_USBFN_ENDPOINT_DIRECTION Direction,
  IN OUT BOOLEAN                  *State
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="endpointindex"></a>*EndpointIndex*  
指示终结点。

<a href="" id="direction"></a>*方向*  
终结点的方向。 有关详细信息，请参阅[EFI\_USBFN\_终结点\_方向](efi-usbfn-endpoint-direction.md)。

<a href="" id="state"></a>*状态*  
一个布尔值;**，则返回 TRUE**值表示的终结点处于已停止状态， **FALSE**否则为。

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


此函数失败，出现**EFI\_无效\_参数**如果指定的方向不正确的终结点。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




