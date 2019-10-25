---
title: KSPROPERTY\_EXTXPORT\_中型\_信息
description: KSPROPERTY\_EXTXPORT\_MEDIUM\_INFO 属性检索有关外部设备介质的信息。
ms.assetid: 04b98c50-ebb0-4224-b476-d261b7c5dd79
keywords:
- KSPROPERTY_EXTXPORT_MEDIUM_INFO 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_MEDIUM_INFO
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3466e28f22a9c3e3ebf749f7079efebfd0460c81
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838062"
---
# <a name="ksproperty_extxport_medium_info"></a>KSPROPERTY\_EXTXPORT\_中型\_信息


KSPROPERTY\_EXTXPORT\_MEDIUM\_INFO 属性检索有关外部设备介质的信息。

## <span id="ddk_ksproperty_extxport_medium_info_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_MEDIUM_INFO_KS"></span>


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
<td><p>无</p></td>
<td><p>设备</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-medium_info" data-raw-source="[&lt;strong&gt;MEDIUM_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-medium_info)"><strong>MEDIUM_INFO</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一种中型\_INFO 结构，描述加载到外部设备中的介质。 例如盒式磁带、磁带级和写保护。

<a name="remarks"></a>备注
-------

KSPROPERTY\_EXTXPORT\_S 结构的**MediumInfo**成员指定信息。

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

[**KSPROPERTY\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

[**中型\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-medium_info)

 

 






