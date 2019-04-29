---
title: CODECAPI\_ALLSETTINGS
description: CODECAPI\_ALLSETTINGS
ms.assetid: 0ae11200-af21-476a-89a8-515bd98920a0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 635cfa5aecfacaa7ff1ba5200196dd290949c509
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374209"
---
# <a name="codecapiallsettings"></a>CODECAPI\_ALLSETTINGS


## <span id="ddk_codecapi_allsettings_ks"></span><span id="DDK_CODECAPI_ALLSETTINGS_KS"></span>


CODECAPI\_ALLSETTINGS 属性用于来回传递微型驱动程序生成的数据块。

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
<td><p>PVOID</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是类型为 PVOID，这是指向微型驱动程序生成的数据块的用户模式缓冲区的指针。

### <a name="comments"></a>备注

在属性上获取调用：

如果应用程序获取使用一个零长度的缓冲区调用的属性，微型驱动程序必须返回状态\_缓冲区\_溢出，并指定所需的缓冲区大小以**Irp-&gt;IoStatus.Information**字段。 如果不为零长度的缓冲区，微型驱动程序必须返回状态\_缓冲区\_过\_小如果所提供的缓冲区太小数据块，否则微型驱动程序包的数据块将其设置可以是稍后还原。

它是微型驱动程序的责任，若要添加的数据完整性检查数据，如要指示微型驱动程序生成的数据、 循环冗余检查 (CRC) 以及标头长度的唯一 GUID。

返回的数据应轻量，并包含仅需重新构造的当前设置的信息。

应用程序将使用此属性的多级撤消，存储其项目等的值。

在属性上设置调用：

微型驱动程序必须验证数据的完整性，并检查数据块大小低于最大数据大小 （例如，拒绝任何特定大小相比）。 它还必须验证 CRC 和标头长度。 微型驱动程序也必须缓存的任何更改的传播[CODECAPI\_CURRENTCHANGELIST](codecapi-currentchangelist.md)。

### <a name="requirements"></a>要求

**标头：** 在中声明*ksmedia.h*。 包括*ksmedia.h*。

### <a name="see-also"></a>请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)， [CODECAPI\_CURRENTCHANGELIST](codecapi-currentchangelist.md)

 

 





