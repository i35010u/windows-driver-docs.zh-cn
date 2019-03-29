---
title: EFI_USBFN_IO_PROTOCOL.FreeTransferBuffer
description: EFI_USBFN_IO_PROTOCOL.FreeTransferBuffer
ms.assetid: 236b925f-2c7b-4df8-b5c8-e8c2f7b853d2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 659ae6f83a21fdf93d1e364b51d1ff7e9e74b4ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564959"
---
# <a name="efiusbfnioprotocolfreetransferbuffer"></a>EFI\_USBFN\_IO\_PROTOCOL.FreeTransferBuffer


**FreeTransferBuffer**函数取消分配的传输缓冲区分配的内存[EFI\_USBFN\_IO\_协议。AllocateTransferBuffer](efi-usbfn-io-protocolallocatetransferbuffer.md)函数。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_FREE_TRANSFER_BUFFER) (
  IN EFI_USBFN_IO_PROTOCOL    *This,
  IN VOID                     *Buffer
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例

<a href="" id="buffer"></a>*缓冲区*  
指向要取消分配的传输缓冲区的指针。

## <a name="return-values"></a>返回值


此函数将返回以下值：

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
</tbody>
</table>

 

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




