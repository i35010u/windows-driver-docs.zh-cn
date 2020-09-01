---
title: CODECAPI \_ ALLSETTINGS
description: CODECAPI \_ ALLSETTINGS
ms.assetid: 0ae11200-af21-476a-89a8-515bd98920a0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4839017cef179897b5a766756cd46c9996326b4f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186383"
---
# <a name="codecapi_allsettings"></a>CODECAPI \_ ALLSETTINGS


## <span id="ddk_codecapi_allsettings_ks"></span><span id="DDK_CODECAPI_ALLSETTINGS_KS"></span>


CODECAPI \_ ALLSETTINGS 属性用于向后传递微型驱动程序生成的数据块。

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
<td><p>PVOID</p></td>
</tr>
</tbody>
</table>

 

操作数据) 的属性值 (的类型为 PVOID，这是一个指向微型驱动程序生成的数据块的用户模式缓冲区的指针。

### <a name="comments"></a>说明

在属性 get 调用上：

如果应用程序使用长度为零的缓冲区进行属性 get 调用，则微型驱动程序必须返回状态 \_ 缓冲区 \_ 溢出，并在 ** &gt; IoStatus** 字段中指定所需的缓冲区大小。 如果长度缓冲区不为零，并且所 \_ \_ 提供的 \_ 缓冲区对于数据块而言太小，则微型驱动程序必须返回状态缓冲区太小，否则，微型驱动程序会将其设置打包到可在以后还原的数据块。

微型驱动程序负责向数据添加数据完整性检查，如用于指示微型驱动程序生成数据的唯一 GUID、循环冗余检查 (CRC) 和标头长度。

返回的数据应为轻型，只包含重建当前设置所需的信息。

应用程序将使用此属性来处理多级 undos，并将其项目等一起存储。

在属性集调用上：

微型驱动程序必须验证数据的完整性并检查数据块大小是否低于最大数据大小 (例如，拒绝超过特定大小) 的任何内容。 它还必须验证 CRC 和标头长度。 微型驱动程序还必须缓存要传播到 [CODECAPI \_ CURRENTCHANGELIST](codecapi-currentchangelist.md)的任何更改。

### <a name="requirements"></a>要求

**标头：** 在 *ksmedia*中声明。 包括 *ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)， [CODECAPI \_ CURRENTCHANGELIST](codecapi-currentchangelist.md)

 

