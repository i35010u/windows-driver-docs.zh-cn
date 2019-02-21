---
title: EFI_USBFN_IO_PROTOCOL.GetVendorIdProductId
description: EFI_USBFN_IO_PROTOCOL.GetVendorIdProductId
ms.assetid: 78dbc589-3ffd-4ee2-9d80-4570b3b20b2f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cc95119621882735c518b36e23b6c1b4affd20a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522204"
---
# <a name="efiusbfnioprotocolgetvendoridproductid"></a>EFI\_USBFN\_IO\_PROTOCOL.GetVendorIdProductId


**GetVendorIdProductId**函数返回的供应商 id 和设备的产品 id。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_GET_VENDOR_ID_PRODUCT_ID) (
  IN EFI_USBFN_IO_PROTOCOL      *This,
  OUT UINT16                    *Vid,
  OUT UINT16                    *Pid
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="vid"></a>*Vid*  
返回供应商的设备的 id。 供应商 Id (Vid) 是由供应商公司拥有的 16 位数字和分配和维护的 USB-如果。

<a href="" id="pid"></a>*pid*  
设备的返回的产品 id。 产品 Id (Pid) 是由每个供应商，他们认为适合的 16 位数字。

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
<td><p><strong>EFI_NOT_FOUND</strong></p></td>
<td><p>无法返回 VID 或 PID。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




