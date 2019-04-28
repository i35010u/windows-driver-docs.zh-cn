---
title: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Initialize
description: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Initialize
ms.assetid: e27ed767-7854-4b2f-8043-35c39357eee4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d97671cbdffee53a43ac7fce5e85d4d6a36ad1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337801"
---
# <a name="efisimplewinphoneioprotocolinitialize"></a>EFI\_SIMPLE\_WINPHONE\_IO\_PROTOCOL.Initialize


**初始化**函数等待指定的秒数从主计算机的连接。 如果不是有效的连接， **EFI\_超时**返回与失败状态。

## <a name="syntax"></a>语法


```cpp
typedef
EFI_STATUS(EFIAPI * EFI_SIMPLE_WINPHONE_IO_INITIALIZE) 
(
  IN EFI_SIMPLE_WINPHONE_IO_PROTOCOL    *This,
  IN UINTN                              ConnectionTimeout,
  IN UINTN                              ReadWriteTimeout
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_简单\_WINPHONE\_IO\_协议实例。

<a href="" id="connectiontimeout"></a>*ConnectionTimeout*  
要从主计算机的连接等待的毫秒数。

<a href="" id="readwritetimeout"></a>*ReadWriteTimeout*  
要等待的读取和写入操作完成的毫秒数。

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
</tbody>
</table>

 

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




