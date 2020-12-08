---
title: EFI_USBFN_IO_PROTOCOL.FreeTransferBuffer
description: EFI_USBFN_IO_PROTOCOL.FreeTransferBuffer
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1f713d6c91956a12d5858eb02068c69da7888d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803375"
---
# <a name="efi_usbfn_io_protocolfreetransferbuffer"></a>EFI \_ USBFN \_ IO \_ 协议。FreeTransferBuffer


**FreeTransferBuffer** 函数取消 [EFI \_ USBFN \_ IO 协议分配给传输缓冲区的内存 \_ 。AllocateTransferBuffer](efi-usbfn-io-protocolallocatetransferbuffer.md)函数。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_FREE_TRANSFER_BUFFER) (
  IN EFI_USBFN_IO_PROTOCOL    *This,
  IN VOID                     *Buffer
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针

<a href="" id="buffer"></a>*宽限*  
指向要取消分配的传输缓冲区的指针。

## <a name="return-values"></a>返回值


此函数返回以下值：

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
</tbody>
</table>

 

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




