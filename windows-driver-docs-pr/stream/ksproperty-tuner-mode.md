---
title: KSPROPERTY\_调谐器\_模式
description: 用户模式客户端使用 KSPROPERTY\_调谐器\_MODE 属性来获取或设置设备的优化模式，如模拟电视、数字电视、FM、AM 或 DSS。 必须实现此属性。
ms.assetid: 84df4030-3836-48de-be83-ecd749839081
keywords:
- KSPROPERTY_TUNER_MODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_MODE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7e3e7891b71f706caafd3309ca3a1cc171f841e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837911"
---
# <a name="ksproperty_tuner_mode"></a>KSPROPERTY\_调谐器\_模式


用户模式客户端使用 KSPROPERTY\_调谐器\_MODE 属性来获取或设置设备的优化模式，如模拟电视、数字电视、FM、AM 或 DSS。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_mode_ks"></span><span id="DDK_KSPROPERTY_TUNER_MODE_KS"></span>


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
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_s)"><strong>KSPROPERTY_TUNER_MODE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 ULONG，指定调谐器的当前优化模式。

<a name="remarks"></a>备注
-------

KSPROPERTY\_调谐器\_\_模式的**模式**成员指定当前调谐器模式。

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

[**KSPROPERTY\_调谐器\_模式\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_s)

 

 






