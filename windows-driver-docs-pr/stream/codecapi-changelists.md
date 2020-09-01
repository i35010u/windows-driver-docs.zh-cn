---
title: CODECAPI \_ CHANGELISTS
description: CODECAPI \_ CHANGELISTS
ms.assetid: c1b65350-32b9-4c94-a6d4-74cb9959d737
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fac2308f4a2126b3716c2dfbb7cc1bd511a132a2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186379"
---
# <a name="codecapi_changelists"></a>CODECAPI \_ CHANGELISTS


## <span id="ddk_codecapi_changelists_ks"></span><span id="DDK_CODECAPI_CHANGELISTS_KS"></span>


CODECAPI \_ CHANGELISTS 事件用于返回因属性 "set" 调用而发生更改的 guid 的列表，例如 [CODECAPI \_ ALLSETTINGS](codecapi-allsettings.md) 和 [CODECAPI \_ SETALLDEFAULTS](codecapi-setalldefaults.md)或编码器设置属性。

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
<th>事件描述符类型</th>
<th>事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>支持 (查询) </p></td>
<td><p>是</p></td>
<td><p>筛选器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

有关 DirectShow 筛选器和 KsProxy 的详细信息，请参阅 [内核流式处理代理](/windows-hardware/drivers/ddi/_stream/index)。

驱动程序使用 AVStream [**KsGenerateEvents**](/windows-hardware/drivers/ddi/ks/nf-ks-ksgenerateevents) 发布更改的 guid 的列表。

### <a name="see-also"></a>另请参阅

[**KsGenerateEvents**](/windows-hardware/drivers/ddi/ks/nf-ks-ksgenerateevents)、 [CODECAPI \_ ALLSETTINGS](codecapi-allsettings.md)、 [CODECAPI \_ SETALLDEFAULTS](codecapi-setalldefaults.md)

 

