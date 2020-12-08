---
title: EFI_USBFN_IO_PROTOCOL.AllocateTransferBuffer
description: EFI_USBFN_IO_PROTOCOL.AllocateTransferBuffer
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 784268879b01e6adb40dc91986697ea38a2ac6c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803379"
---
# <a name="efi_usbfn_io_protocolallocatetransferbuffer"></a>EFI \_ USBFN \_ IO \_ 协议。AllocateTransferBuffer


**AllocateTransferBuffer** 函数分配指定大小的传输缓冲区，该缓冲区满足控制器要求。

必须使用对 **FreeTransferBuffer** 函数的匹配调用来释放已分配的传输缓冲区。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_ALLOCATE_TRANSFER_BUFFER) (
  IN EFI_USBFN_IO_PROTOCOL    *This,
  IN UINTN                    Size,
  OUT VOID                    **Buffer
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ USBFN \_ IO \_ 协议实例的指针。

<a href="" id="size"></a>*规格*  
要为传输缓冲区分配的字节数。

<a href="" id="buffer"></a>*宽限*  
如果调用成功，则为指向已分配缓冲区的指针的指针;否则未定义。

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
<tr class="odd">
<td><p><strong>EFI_OUT_OF_RESOURCES</strong></p></td>
<td><p>无法分配请求的传输缓冲区。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




