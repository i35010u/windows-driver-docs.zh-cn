---
title: EFI_USBFN_IO_PROTOCOL.AbortTransfer
description: EFI_USBFN_IO_PROTOCOL.AbortTransfer
ms.assetid: 204998d6-7d8d-482b-8d9c-b96d2e2729bf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb5e2fe98d7070a4ebba1a56f9690d8437634aa9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563316"
---
# <a name="efiusbfnioprotocolaborttransfer"></a>EFI\_USBFN\_IO\_PROTOCOL.AbortTransfer


**AbortTransfer**函数中止在指定的终结点上的传输。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_ABORT_TRANSFER) (
  IN EFI_USBFN_IO_PROTOCOL        *This,
  IN UINT8                        EndpointIndex,
  IN EFI_USBFN_ENDPOINT_DIRECTION Direction
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例

<a href="" id="endpointindex"></a>*EndpointIndex*  
指示需要取消正在进行传输的终结点。

<a href="" id="direction"></a>*方向*  
终结点的方向。 有关详细信息请参阅[EFI\_USBFN\_终结点\_方向](efi-usbfn-endpoint-direction.md)。

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

 

 




