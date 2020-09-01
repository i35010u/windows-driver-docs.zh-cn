---
title: KSPROPERTY \_ COPY \_ MACROVISION
description: KSPROPERTY \_ COPY \_ MACROVISION 属性指示数据流的 MACROVISION 级别。
ms.assetid: 6863bcf6-06bc-4bd2-896e-43c083aa07d5
keywords:
- KSPROPERTY_COPY_MACROVISION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_COPY_MACROVISION
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c09e69fcadf0ba59eec494cb6a1e49e783d98618
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187368"
---
# <a name="ksproperty_copy_macrovision"></a>KSPROPERTY \_ COPY \_ MACROVISION


KSPROPERTY \_ COPY \_ MACROVISION 属性指示数据流的 MACROVISION 级别。

## <span id="ddk_ksproperty_copy_macrovision_ks"></span><span id="DDK_KSPROPERTY_COPY_MACROVISION_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision" data-raw-source="[&lt;strong&gt;KS_COPY_MACROVISION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision)"><strong>KS_COPY_MACROVISION</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KS \_ COPY \_ MACROVISION 结构，该结构指定数据流的 MACROVISION 级别。

<a name="remarks"></a>注解
-------

有关 Macrovision 级别的详细信息，请参阅 [DVD 版权保护](./dvd-copyright-protection.md)。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KS \_ 复制 \_ MACROVISION**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision)

 

