---
title: KSPROPERTY\_VIDEOPROCAMP\_背光\_补偿
description: KSPROPERTY\_VIDEOPROCAMP\_背光\_酬薪属性控制相机上的轻型补偿设置。 此属性为可选项。
ms.assetid: d893fc01-048a-4f2e-8587-d71be0796dcc
keywords:
- KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d86f4f2131a3f23febdee16db88d508e90b0486e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837861"
---
# <a name="ksproperty_videoprocamp_backlight_compensation"></a>KSPROPERTY\_VIDEOPROCAMP\_背光\_补偿


KSPROPERTY\_VIDEOPROCAMP\_背光\_酬薪属性控制相机上的轻型补偿设置。 此属性为可选项。

## <span id="ddk_ksproperty_videoprocamp_backlight_compensation_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION_KS"></span>


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
<td><p>筛选器或节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>漫长</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定相机的后轻补偿设置的 LONG。 此值可以是0或1。 此属性的默认值为1。 如果值为0，则表示禁用了回退轻型补偿。 默认值为1，表示已启用后轻补偿。

<a name="remarks"></a>备注
-------

KSPROPERTY\_VIDEOPROCAMP\_S 结构的**值**成员指定是否启用或禁用背光补偿。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOPROCAMP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)

 

 






