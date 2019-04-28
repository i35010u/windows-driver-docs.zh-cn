---
title: EFI_USBFN_IO_PROTOCOL.AllocateTransferBuffer
description: EFI_USBFN_IO_PROTOCOL.AllocateTransferBuffer
ms.assetid: dbaa4f18-97b5-4867-9e03-de19b2253722
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a2123eb4e494cc8b9362d96b34d8c7822e94442
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337720"
---
# <a name="efiusbfnioprotocolallocatetransferbuffer"></a>EFI\_USBFN\_IO\_PROTOCOL.AllocateTransferBuffer


**AllocateTransferBuffer**函数分配满足控制器要求指定大小的传输缓冲区。

必须使用匹配调用释放已分配的传输缓冲区**FreeTransferBuffer**函数。

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

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_USBFN\_IO\_协议实例。

<a href="" id="size"></a>*大小*  
要为传输缓冲区分配的字节数。

<a href="" id="buffer"></a>*缓冲区*  
指针到指向分配的缓冲区，如果调用成功;否则未定义。

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
<tr class="odd">
<td><p><strong>EFI_OUT_OF_RESOURCES</strong></p></td>
<td><p>无法分配请求的传输缓冲区。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




