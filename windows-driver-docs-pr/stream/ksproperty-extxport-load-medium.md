---
title: KSPROPERTY\_EXTXPORT\_LOAD\_MEDIUM
description: KSPROPERTY\_EXTXPORT\_加载\_中等属性设置或获取外部设备的负载。 对于弹出的示例，请打开送纸器、 关闭送纸器，等等。
ms.assetid: 13ec61ae-4be7-4af6-875f-a6ca178cf6bc
keywords:
- KSPROPERTY_EXTXPORT_LOAD_MEDIUM 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_LOAD_MEDIUM
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 978252ff18fe7df472422be6f16888da4caba939
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354848"
---
# <a name="kspropertyextxportloadmedium"></a>KSPROPERTY\_EXTXPORT\_LOAD\_MEDIUM


KSPROPERTY\_EXTXPORT\_加载\_中等属性设置或获取外部设备的负载。 对于弹出的示例，请打开送纸器、 关闭送纸器，等等。

## <span id="ddk_ksproperty_extxport_load_medium_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_LOAD_MEDIUM_KS"></span>


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
<td><p>设备</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定的当前负载介质的 ULONG。 例如弹出，再打开送纸器或已关闭的送纸器。

<a name="remarks"></a>备注
-------

**LoadMedium** KSPROPERTY 成员\_EXTXPORT\_S 结构指定的负载介质。

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

[**KSPROPERTY\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extxport_s)

 

 






