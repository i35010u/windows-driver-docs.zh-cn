---
title: CODECAPI\_CURRENTCHANGELIST
description: CODECAPI\_CURRENTCHANGELIST
ms.assetid: f783857f-d1a1-417f-8f69-198b6f328a69
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ae314793bae53c9805e7b632533d181ee092ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524133"
---
# <a name="codecapicurrentchangelist"></a>CODECAPI\_CURRENTCHANGELIST


## <span id="ddk_codecapi_currentchangelist_ks"></span><span id="DDK_CODECAPI_CURRENTCHANGELIST_KS"></span>


CODECAPI\_CURRENTCHANGELIST 属性用于指示哪些参数中的上一个属性的"设置"调用，如更改[CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)和[CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)。

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
<td><p>Guid 的数组</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 Guid 的数组。

### <a name="comments"></a>备注

在属性上获取调用：

如果应用程序获取调用具有非零值的缓冲区大小的属性，微型驱动程序将返回状态\_缓冲区\_过\_小如果所提供的缓冲区太小数据块。 如果没有要返回的项，微型驱动程序将返回状态\_成功。 否则返回 Guid 的列表 （即，其中 sizeof(GUID) 字节数等于 16 个字节）。 返回的大小是以字节为单位列表的长度 (即，GUID 数目\*sizeof(GUID))。

在属性上设置调用：

重置已更改的 Guid 的当前列表。

### <a name="requirements"></a>要求

**标头：** 在中声明*ksmedia.h*。 包括*ksmedia.h*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)， [CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)， [CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)

 

 





