---
title: EFI_USBFN_IO_PROTOCOL.GetVendorIdProductId
description: EFI_USBFN_IO_PROTOCOL.GetVendorIdProductId
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7a86b3cf07484eef564bba800e957b2e6e2bfda
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803366"
---
# <a name="efi_usbfn_io_protocolgetvendoridproductid"></a>EFI \_ USBFN \_ IO \_ 协议。GetVendorIdProductId


**GetVendorIdProductId** 函数返回设备的供应商 id 和产品 id。

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
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

<a href="" id="vid"></a>*Vid*  
返回的设备的供应商 id。  (VIDs) 的供应商 Id 是供应商公司拥有的16位数字，由 USB-IF 分配和维护。

<a href="" id="pid"></a>*P&id*  
返回的设备的产品 id。 产品 Id (Pid) 为每个供应商分配的16位数字。

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
<td><p><strong>EFI_NOT_FOUND</strong></p></td>
<td><p>无法返回 VID 或 PID。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




