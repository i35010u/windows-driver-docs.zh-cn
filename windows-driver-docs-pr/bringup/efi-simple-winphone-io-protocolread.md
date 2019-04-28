---
title: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Read
description: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Read
ms.assetid: 9b5525a4-d98c-4328-8ebe-55ede53befca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b71ff27f2e13acb8a3c6076382658f75e9bcd4b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337789"
---
# <a name="efisimplewinphoneioprotocolread"></a>EFI\_SIMPLE\_WINPHONE\_IO\_PROTOCOL.Read


**读取**函数从设备中读取数据。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_SIMPLE_WINPHONE_IO_READ) (
  IN EFI_SIMPLE_WINPHONE_IO_PROTOCOL    *This,
  IN UINTN                              NumberOfBytesToRead,
  IN OUT UINTN                          *NumberOfBytesRead,
  OUT VOID                              *Buffer
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_简单\_WINPHONE\_IO\_协议实例。

<a href="" id="numberofbytestoread"></a>*NumberOfBytesToRead*  
要读取的字节数目上限。

<a href="" id="numberofbytesread"></a>*NumberOfBytesRead*  
返回以字节为单位的缓冲区中的数据量

<a href="" id="buffer"></a>*缓冲区*  
要返回到的数据的缓冲区。

## <a name="return-values"></a>返回值


该函数返回以下值之一：

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
<tr class="odd">
<td><p><strong>EFI_TIMEOUT</strong></p></td>
<td><p>建立连接之前发生超时。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_NO_RESPONSE</strong></p></td>
<td><p>与主机的连接不存在或已终止。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


所需的数据是可用或在超时之前，将阻止此函数。

如果出错，将读取任何字节，并将返回相应的状态代码。 在所有情况下，在返回实际读取的字节数**NumberOfBytesRead**。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




