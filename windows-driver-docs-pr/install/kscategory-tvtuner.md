---
title: KSCATEGORY_TVTUNER
description: KSCATEGORY_TVTUNER
ms.assetid: 44d9d407-a94c-40de-b749-af50bc5718f4
keywords:
- KSCATEGORY_TVTUNER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_TVTUNER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 78e5b04ccb3a57b1566fc5a785218ca88e8cc553
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520980"
---
# <a name="kscategorytvtuner"></a>KSCATEGORY_TVTUNER


KSCATEGORY_TVTUNER[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)电视调谐器设备 (KS) 功能类别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_TVTUNER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{A799A800-A46D-11D0-A18C-00A02401DCD4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_TVTUNER 向操作系统指示设备支持 KSCATEGORY_TVTUNER 功能分类的实例。

有关如何在一个 INF 文件中注册此功能的类别的示例，请参阅*Bdan.inf* INF 文件，包括中的软件调谐器示例*src/swtuner/algtuner* WDK 的目录。

视频设备有关的信息，请参阅[视频捕获设备](https://msdn.microsoft.com/library/windows/hardware/ff568699)，[筛选器关系图示例](https://msdn.microsoft.com/library/windows/hardware/ff559605)，并[编码器设备](https://msdn.microsoft.com/library/windows/hardware/ff559535)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSCATEGORY_TVAUDIO**](kscategory-tvaudio.md)

 

 






