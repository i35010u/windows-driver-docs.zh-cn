---
title: CODECAPI \_ SUPPORTSEVENTS
description: CODECAPI \_ SUPPORTSEVENTS
ms.assetid: feb6d110-9a9c-4e2b-bc19-259f80f3947a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a82bfb3801870b513ed340f448de3eb509cd3568
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186349"
---
# <a name="codecapi_supportsevents"></a>CODECAPI \_ SUPPORTSEVENTS


## <span id="ddk_codecapi_supportsevents_ks"></span><span id="DDK_CODECAPI_SUPPORTSEVENTS_KS"></span>


CODECAPI \_ SUPPORTSEVENTS 属性用于指示微型驱动程序是否支持用户模式事件。 也就是说，微型驱动程序实现 [CODECAPI \_ CHANGELISTS](codecapi-changelists.md) 事件。

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
<th>获取</th>
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
<td><p>筛选器</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 BOOL 类型，它指定微型驱动程序是否支持用户模式事件。 如果值为 **TRUE** ，则表示微型驱动程序提供支持。 如果微型驱动程序不支持事件机制，则不应支持此 GUID。

### <a name="requirements"></a>要求

**标头：** 在 *ksmedia*中声明。 包括 *ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

