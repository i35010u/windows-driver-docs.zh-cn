---
title: CODECAPI \_ CURRENTCHANGELIST
description: CODECAPI \_ CURRENTCHANGELIST
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc5f52f44d829f7e24540dd530b43369799d532a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795379"
---
# <a name="codecapi_currentchangelist"></a>CODECAPI \_ CURRENTCHANGELIST


## <span id="ddk_codecapi_currentchangelist_ks"></span><span id="DDK_CODECAPI_CURRENTCHANGELIST_KS"></span>


CODECAPI \_ CURRENTCHANGELIST 属性用于指示在前一个属性 "set" 调用中更改了哪些参数，如 [CODECAPI \_ ALLSETTINGS](codecapi-allsettings.md) 和 [CODECAPI \_ SETALLDEFAULTS](codecapi-setalldefaults.md)。

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
<td><p>Guid 数组</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 Guid 数组。

### <a name="comments"></a>注释

在属性 get 调用上：

如果应用程序使用非零缓冲区大小进行属性 get 调用，并且所 \_ \_ 提供的 \_ 缓冲区对于数据块而言太小，则微型驱动程序返回的状态缓冲区太小。 如果没有要返回的项，则微型驱动程序将返回状态 " \_ 成功"。 否则，将返回 Guid 列表 (即，sizeof (GUID) 字节等于16字节) 。 返回的大小是列表的长度（以字节为单位） (即 guid \* sizeof (guid) # A3 的数目。

在属性集调用上：

已更改的 Guid 的当前列表已重置。

### <a name="requirements"></a>要求

**标头：** 在 *ksmedia* 中声明。 包括 *ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)、 [CODECAPI \_ ALLSETTINGS](codecapi-allsettings.md)、 [CODECAPI \_ SETALLDEFAULTS](codecapi-setalldefaults.md)

 

