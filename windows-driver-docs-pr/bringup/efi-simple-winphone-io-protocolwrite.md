---
title: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Write
description: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Write
ms.assetid: 55475573-e904-4adc-91cf-62afe9e67927
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24ebe500efe1da3cc058369c84b341f1bbf7c0c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337758"
---
# <a name="efisimplewinphoneioprotocolwrite"></a>EFI\_SIMPLE\_WINPHONE\_IO\_PROTOCOL.Write


**编写**函数将数据写入到设备。

所需的数据写入到设备或在超时之前，将阻止此函数。

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

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_简单\_WINPHONE\_IO\_协议实例

<a href="" id="numberofbytestowrite"></a>*NumberOfBytesToWrite*  
要写入到设备的字节数。

<a href="" id="numberofbyteswritten"></a>*NumberOfBytesWritten*  
实际写入以字节为单位的数据量。

<a href="" id="buffer"></a>*缓冲区*  
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


如果出错，传输将因相应的状态代码。 在所有情况下，在返回实际写入到设备的字节数**NumberOfBytesWritten**。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




