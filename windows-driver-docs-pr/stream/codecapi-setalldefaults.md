---
title: CODECAPI \_ SETALLDEFAULTS
description: CODECAPI \_ SETALLDEFAULTS
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73fa061b4da3c15c3cacd73a03e951150d86e28f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792523"
---
# <a name="codecapi_setalldefaults"></a>CODECAPI \_ SETALLDEFAULTS


## <span id="ddk_codecapi_setalldefaults_ks"></span><span id="DDK_CODECAPI_SETALLDEFAULTS_KS"></span>


CODECAPI \_ SETALLDEFAULTS 属性用于将微型驱动程序的所有内部设置重置为其默认配置。

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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>筛选器</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>

 

设置为此属性集的是一个触发器，设备应将其所有设置重置为默认值。

### <a name="comments"></a>注释

设置此属性时，微型驱动程序应为 [CODECAPI \_ CURRENTCHANGELIST](codecapi-currentchangelist.md) 缓存已更改参数的整个列表。

### <a name="requirements"></a>要求

**标头：** 在 *ksmedia* 中声明。 包括 *ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

