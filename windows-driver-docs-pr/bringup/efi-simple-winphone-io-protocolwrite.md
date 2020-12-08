---
title: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Write
description: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Write
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 055ad32f874b83d0d2dfa458a790ee04fefba689
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803395"
---
# <a name="efi_simple_winphone_io_protocolwrite"></a>EFI \_ 简单 \_ WINPHONE \_ IO \_ 协议。写入


**写入** 函数会将数据写入设备。

此函数将被阻止，直到将请求的数据量写入设备或超时。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_SIMPLE_WINPHONE_IO_WRITE) (
  IN EFI_SIMPLE_WINPHONE_IO_PROTOCOL    *This,
  IN UINTN                              NumberOfBytesToWrite,
  IN OUT UINTN                          *NumberOfBytesWritten,
  IN VOID                               *Buffer
  );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
指向 EFI \_ 简单 \_ WINPHONE \_ IO \_ 协议实例的指针

<a href="" id="numberofbytestowrite"></a>*NumberOfBytesToWrite*  
要写入设备的字节数。

<a href="" id="numberofbyteswritten"></a>*NumberOfBytesWritten*  
实际写入的数据量（以字节为单位）。

<a href="" id="buffer"></a>*宽限*  
要写入的数据的缓冲区。

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
<tr class="odd">
<td><p><strong>EFI_TIMEOUT</strong></p></td>
<td><p>建立连接之前出现超时。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_NO_RESPONSE</strong></p></td>
<td><p>与主机的连接不存在或已被终止。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


如果发生错误，将以适当的状态代码终止传输。 在所有情况下，都将在 **NumberOfBytesWritten** 中返回实际写入设备的字节数。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




