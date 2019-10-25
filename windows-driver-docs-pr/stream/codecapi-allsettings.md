---
title: CODECAPI\_ALLSETTINGS
description: CODECAPI\_ALLSETTINGS
ms.assetid: 0ae11200-af21-476a-89a8-515bd98920a0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31d92b135efd6bfbfddd3446d06c159643d75c92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844731"
---
# <a name="codecapi_allsettings"></a>CODECAPI\_ALLSETTINGS


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
<td><p>PVOID</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 PVOID，这是一个指向微型驱动程序生成的数据块的用户模式缓冲区的指针。

### <a name="comments"></a>备注

在属性 get 调用上：

如果应用程序使用长度为零的缓冲区进行属性 get 调用，则微型驱动程序必须返回状态\_缓冲区\_溢出，并在**Irp-&gt;IoStatus**字段中指定所需的缓冲区大小。 如果长度缓冲区为非零值，则微型驱动程序必须返回状态\_缓冲区\_\_如果为数据块提供的缓冲区太小，则必须将其设置打包到可在以后还原的数据块。

微型驱动程序负责向数据添加数据完整性检查，如用于指示微型驱动程序生成数据的唯一 GUID、循环冗余检查（CRC）和标头长度。

返回的数据应为轻型，只包含重建当前设置所需的信息。

应用程序将使用此属性来处理多级 undos，并将其项目等一起存储。

在属性集调用上：

微型驱动程序必须验证数据的完整性并检查数据块大小是否低于最大数据大小（例如，拒绝某个大小的任何内容）。 它还必须验证 CRC 和标头长度。 微型驱动程序还必须缓存要为[CODECAPI\_CURRENTCHANGELIST](codecapi-currentchangelist.md)传播的任何更改。

### <a name="requirements"></a>要求

**标头：** 在*ksmedia*中声明。 包括*ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)、 [CODECAPI\_CURRENTCHANGELIST](codecapi-currentchangelist.md)

 

 





