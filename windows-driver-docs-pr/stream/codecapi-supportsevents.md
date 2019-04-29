---
title: CODECAPI\_SUPPORTSEVENTS
description: CODECAPI\_SUPPORTSEVENTS
ms.assetid: feb6d110-9a9c-4e2b-bc19-259f80f3947a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3add63d9a6c4d1be086762aff919358a7f7fa00e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372789"
---
# <a name="codecapisupportsevents"></a>CODECAPI\_SUPPORTSEVENTS


## <span id="ddk_codecapi_supportsevents_ks"></span><span id="DDK_CODECAPI_SUPPORTSEVENTS_KS"></span>


CODECAPI\_SUPPORTSEVENTS 属性用来指示微型驱动程序是否支持用户模式事件。 也就是说，微型驱动程序实现[CODECAPI\_包括](codecapi-changelists.md)事件。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值是布尔值，指定是否微型驱动程序支持用户模式事件类型。 值为 **，则返回 TRUE**指示微型驱动程序提供支持。 如果不支持的事件机制，微型驱动程序应支持此 GUID。

### <a name="requirements"></a>要求

**标头：** 在中声明*ksmedia.h*。 包括*ksmedia.h*。

### <a name="see-also"></a>请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 





