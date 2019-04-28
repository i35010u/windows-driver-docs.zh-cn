---
title: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.GetMaxPacketSize
description: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.GetMaxPacketSize
ms.assetid: 8808bb5d-e00d-4b19-87ad-4a071a896e22
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 473395ba84360980f2a279e56a2a1b420fb3e21e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337793"
---
# <a name="efisimplewinphoneioprotocolgetmaxpacketsize"></a>EFI\_SIMPLE\_WINPHONE\_IO\_PROTOCOL.GetMaxPacketSize


**GetMaxPacketSize**函数返回的最大可以容纳在单个的字节数读取或写入操作。

## <a name="syntax"></a>语法


```cpp
typedef 
EFI_STATUS 
(EFIAPI * EFI_SIMPLE_WINPHONE_IO_GET_MAXPACKET_SIZE) ( 
  IN EFI_SIMPLE_WINPHONE_IO_PROTOCOL    *This, 
  OUT UINTN                             *MaxPacketSize 
  );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
指向 EFI\_简单\_WINPHONE\_IO\_协议实例。

<a href="" id="maxpacketsize"></a>*MaxPacketSize*  
支持的最大数据包大小，以字节为单位。

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
</tbody>
</table>

 

## <a name="remarks"></a>备注


## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




