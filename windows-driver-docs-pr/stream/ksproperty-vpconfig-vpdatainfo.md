---
title: KSPROPERTY \_ VPCONFIG \_ VPDATAINFO
description: KSPROPERTY \_ VPCONFIG \_ VPDATAINFO 属性指示视频端口的初始配置状态。
ms.assetid: 66419d5a-c701-45f4-9ac6-322997e2f000
keywords:
- KSPROPERTY_VPCONFIG_VPDATAINFO 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_VPDATAINFO
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50a33fa0304f0bf86310c5a23ba038dd53990f2c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103628"
---
# <a name="ksproperty_vpconfig_vpdatainfo"></a>KSPROPERTY \_ VPCONFIG \_ VPDATAINFO


KSPROPERTY \_ VPCONFIG \_ VPDATAINFO 属性指示视频端口的初始配置状态。

## <span id="ddk_ksproperty_vpconfig_vpdatainfo_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_VPDATAINFO_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

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
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_amvpdatainfo" data-raw-source="[&lt;strong&gt;KS_AMVPDATAINFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_amvpdatainfo)"><strong>KS_AMVPDATAINFO</strong></a></p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是 \_ 用于描述视频端口属性的 KS AMVPDATAINFO 结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KS \_ AMVPDATAINFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_amvpdatainfo)

