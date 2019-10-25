---
title: CODECAPI\_SETALLDEFAULTS
description: CODECAPI\_SETALLDEFAULTS
ms.assetid: 6a50a75f-cbc5-487f-b2cd-34e89eb127a0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c18ba4f9f5bf5b3f02da0c13f26a46171e47be37
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844723"
---
# <a name="codecapi_setalldefaults"></a>CODECAPI\_SETALLDEFAULTS


## <span id="ddk_codecapi_setalldefaults_ks"></span><span id="DDK_CODECAPI_SETALLDEFAULTS_KS"></span>


CODECAPI\_SETALLDEFAULTS 属性用于将微型驱动程序的所有内部设置重置为其默认配置。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>

 

设置为此属性集的是一个触发器，设备应将其所有设置重置为默认值。

### <a name="comments"></a>备注

设置此属性时，微型驱动程序应缓存[CODECAPI\_CURRENTCHANGELIST](codecapi-currentchangelist.md)的已更改参数的整个列表。

### <a name="requirements"></a>要求

**标头：** 在*ksmedia*中声明。 包括*ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 





