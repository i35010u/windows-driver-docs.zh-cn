---
title: KSPROPERTY \_ 调谐器 \_ 标准版
description: KSPROPERTY \_ 调谐器 \_ 标准属性检索当前的模拟视频标准。 必须实现此属性。
keywords:
- KSPROPERTY_TUNER_STANDARD 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_STANDARD
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73bb337bfb00b9f0f1d713894882e0dc8c855aa1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837609"
---
# <a name="ksproperty_tuner_standard"></a>KSPROPERTY \_ 调谐器 \_ 标准版


KSPROPERTY \_ 调谐器 \_ 标准属性检索当前的模拟视频标准。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_standard_ks"></span><span id="DDK_KSPROPERTY_TUNER_STANDARD_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_s)"><strong>KSPROPERTY_TUNER_STANDARD_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 ULONG，用于指定调谐器的优化标准。

<a name="remarks"></a>备注
-------

KSPROPERTY 调谐器标准版结构的 **标准** 成员 \_ \_ \_ 指定当前的模拟视频标准。

仅当当前模式为 KSPROPERTY 调谐器模式时，才使用此属性 \_ \_ \_ 。

可以按照多种不同的模拟电视标准（例如 NTSC、PAL 或 SECAM）来广播模拟电视信号。 客户端使用 KSPROPERTY \_ 调谐器 \_ MODE \_ cap 属性来查询支持的标准，并使用 KSPROPERTY \_ 调谐器 \_ 标准获取或设置电视调谐器设备的当前标准。

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

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ 调谐器 \_ 标准版 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_s)

[**KSPROPERTY \_ 调谐器 \_ 模式**](ksproperty-tuner-mode.md)

