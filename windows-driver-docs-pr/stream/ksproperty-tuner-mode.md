---
title: KSPROPERTY\_TUNER\_MODE
description: 用户模式下客户端使用 KSPROPERTY\_调谐器\_模式属性来获取或设置的设备，如模拟电视、 数字电视、 FM、 AM、 优化模式或 DSS。 必须实现此属性。
ms.assetid: 84df4030-3836-48de-be83-ecd749839081
keywords:
- KSPROPERTY_TUNER_MODE 流式处理媒体设备
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
ms.openlocfilehash: 6e9df3e6ec8ac23a883b5d75a7a9dd2f5e2a09a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342203"
---
# <a name="kspropertytunermode"></a>KSPROPERTY\_TUNER\_MODE


用户模式下客户端使用 KSPROPERTY\_调谐器\_模式属性来获取或设置的设备，如模拟电视、 数字电视、 FM、 AM、 优化模式或 DSS。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_mode_ks"></span><span id="DDK_KSPROPERTY_TUNER_MODE_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565878" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565878)"><strong>KSPROPERTY_TUNER_MODE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 ULONG，用于指定调谐器的当前优化模式。

<a name="remarks"></a>备注
-------

**模式下**KSPROPERTY 成员\_调谐器\_模式\_S 结构指定的当前调谐器模式。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_调谐器\_模式\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565878)

 

 






