---
title: KSCATEGORY_VIDEO
description: KSCATEGORY_VIDEO
ms.assetid: cdcdb22b-3969-4c58-a8ce-a9d0b4b64e3b
keywords:
- KSCATEGORY_VIDEO 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_VIDEO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0c972856e24ea2ceec3104ec3ae79dd5bf1f3e9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330534"
---
# <a name="kscategoryvideo"></a>KSCATEGORY_VIDEO


KSCATEGORY_VIDEO[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)视频设备 (KS) 功能类别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_VIDEO</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{6994AD05-93EF-11D0-A3CC-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 视频设备的驱动程序注册 KSCATEGORY_VIDEO 向操作系统指示设备支持 KSCATEGORY_VIDEO 功能分类的实例。

有关如何在一个 INF 文件中注册此功能的类别的示例，请参阅*Bdan.inf* INF 文件，包括中的软件调谐器示例*src/swtuner/algtuner* WDK 的目录。

有关此功能的类别的详细信息，请参阅[提供 UVC INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff568123)。

有关视频设备的常规信息，请参阅[视频捕获设备](https://msdn.microsoft.com/library/windows/hardware/ff568699)。

有关视频设备其他设备接口类的信息，请参阅[ **KSCATEGORY_TVAUDIO** ](kscategory-tvaudio.md)并[ **KSCATEGORY_TVTUNER** ](kscategory-tvtuner.md).

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSCATEGORY_TVAUDIO**](kscategory-tvaudio.md)

[**KSCATEGORY_TVTUNER**](kscategory-tvtuner.md)

 

 






