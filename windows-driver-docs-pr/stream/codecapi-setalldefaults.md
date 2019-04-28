---
title: CODECAPI\_SETALLDEFAULTS
description: CODECAPI\_SETALLDEFAULTS
ms.assetid: 6a50a75f-cbc5-487f-b2cd-34e89eb127a0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 227c525dd078f6167c386a43aeab613e9af3a44c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329605"
---
# <a name="codecapisetalldefaults"></a>CODECAPI\_SETALLDEFAULTS


## <span id="ddk_codecapi_setalldefaults_ks"></span><span id="DDK_CODECAPI_SETALLDEFAULTS_KS"></span>


CODECAPI\_SETALLDEFAULTS 属性用于微型驱动程序的所有内部设置重置为其默认配置。

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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>

 

设置此属性设置为是，设备应重置所有其设置为其默认值的触发器。

### <a name="comments"></a>备注

微型驱动程序应缓存其整个列表已更改的参数[CODECAPI\_CURRENTCHANGELIST](codecapi-currentchangelist.md)时设置此属性。

### <a name="requirements"></a>要求

**标头：** 在中声明*ksmedia.h*。 包括*ksmedia.h*。

### <a name="see-also"></a>请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 





