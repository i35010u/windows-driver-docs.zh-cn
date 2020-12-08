---
title: CODECAPI \_ SUPPORTSEVENTS
description: CODECAPI \_ SUPPORTSEVENTS
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59bb2fdad1a8d4d0785c73abc6625fce5d7537a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804375"
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

**标头：** 在 *ksmedia* 中声明。 包括 *ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

