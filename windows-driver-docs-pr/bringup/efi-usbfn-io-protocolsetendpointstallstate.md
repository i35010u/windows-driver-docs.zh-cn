---
title: EFI_USBFN_IO_PROTOCOL.SetEndpointStallState
description: EFI_USBFN_IO_PROTOCOL.SetEndpointStallState
ms.assetid: bd754296-5002-48b6-9986-fa09c2094470
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1f2df4b3b5f81bc2e9b78ea27c9b306b83e9f5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337673"
---
# <a name="efiusbfnioprotocolsetendpointstallstate"></a>EFI\_USBFN\_IO\_PROTOCOL.SetEndpointStallState


**SetEndpointStallState**函数设置或清除指定的终结点上的停止状态。

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

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="endpointindex"></a>*EndpointIndex*  
指示需要已停止的终结点。

<a href="" id="direction"></a>*方向*  
终结点的方向。 有关详细信息，请参阅[EFI\_USBFN\_终结点\_方向](efi-usbfn-endpoint-direction.md)。

<a href="" id="state"></a>*状态*  
请求指定的终结点上停止状态。 此参数设置为 **，则返回 TRUE**导致要停止的终结点。 将其设置为**FALSE**清除现有停滞。

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

 

 




