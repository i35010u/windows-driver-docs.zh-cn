---
title: CODECAPI\_CURRENTCHANGELIST
description: CODECAPI\_CURRENTCHANGELIST
ms.assetid: f783857f-d1a1-417f-8f69-198b6f328a69
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c83cbb7ab2f2968ee0f5c150244dacf6d8d9b24e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844726"
---
# <a name="codecapi_currentchangelist"></a>CODECAPI\_CURRENTCHANGELIST


## <span id="ddk_codecapi_currentchangelist_ks"></span><span id="DDK_CODECAPI_CURRENTCHANGELIST_KS"></span>


CODECAPI\_CURRENTCHANGELIST 属性用于指示在前一个属性 "set" 调用中更改了哪些参数，如[CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)和[CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)。

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
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>Guid 数组</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 Guid 数组。

### <a name="comments"></a>备注

在属性 get 调用上：

如果应用程序使用非零缓冲区大小进行属性 get 调用，则当所提供的缓冲区对于数据块而言太小时，微型驱动程序将返回状态\_缓冲区\_太小\_。 如果没有要返回的项，则微型驱动程序将返回状态\_SUCCESS。 否则，将返回 Guid 列表（即，sizeof （GUID）字节数等于16个字节）。 返回的大小是列表的长度（以字节为单位，即 GUID \* sizeof （GUID））的数目。

在属性集调用上：

已更改的 Guid 的当前列表已重置。

### <a name="requirements"></a>要求

**标头：** 在*ksmedia*中声明。 包括*ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)、 [CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)、 [CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)

 

 





